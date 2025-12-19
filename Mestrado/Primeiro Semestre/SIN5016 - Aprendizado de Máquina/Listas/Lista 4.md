# Otimização irrestrita da função de Rosebrock $(N=3)$
Função de Rosebrock:
$$
	f(x) = \displaystyle\sum_{i=1}^{N-1} [100(x_{i+1} - x_i²)^2+ (1 - x_i)²], x \in \reals^N
$$
$$
	f(x) = \displaystyle\sum_{i=1}^{2} [100(x_{i+1} - x_i²)^2+ (1 - x_i)²], x \in \reals^3
$$

O mínimo global ocorre em $(1, 1, 1)$, com $f = 0$

# Aproximação do Gradiente e da Hessiana
O Gradiente e a Hessiana foram aproximados por diferenças finitas centrais, usando um passo pequeno de $h$.
* Gradiente:
$$
	{\partial f \over \partial x_i} (x) \approx {{f(x + he_i) - f(x- he_i)} \over 2h}
$$
* Hessiana:
$$
	{\partial² f \over \partial x_i²} (x) \approx {{f(x + he_i) - 2f(x) + f(x - he_i)} \over h²}
$$
$$
	{\partial² f \over {\partial x_i \partial x_j}} (x) \approx {{f(x + he_i + he_j) - f(x + he_i - he_j) - f(x - he_i + he_j) + f(x - he_i - he_j)} \over 4h²}
$$

Foram utilizados valores típicos $h = 10^{-6}$ para o gradeinte e $h = 10^{-4}$ para a Hessiana

# Métodos utilizados
Foram implementados os seguintes métodos de otimização irrestrita:
 * **Gradiente descendente**, com escolha do passo via busca linera (razão áurea);
 * **Método de Newton**, com Hessiana aproximada, positivação da matriz e backtracking;
 * **Quasi-Newton (BFGS)**, com atualização da aproximação da Hessiana inversa e busca linear.

```python
import numpy as np

# ============================================================
# Rosenbrock N=3
# f(x1,x2,x3) = 100(x2-x1^2)^2 + (1-x1)^2 + 100(x3-x2^2)^2 + (1-x2)^2
# mínimo global: (1,1,1), f=0
# ============================================================

def rosenbrock3(x: np.ndarray) -> float:
    x1, x2, x3 = x
    return 100.0*(x2 - x1**2)**2 + (1.0 - x1)**2 + 100.0*(x3 - x2**2)**2 + (1.0 - x2)**2


# ============================================================
# Diferenças finitas (centrais)
# ============================================================

def approx_grad(f, x, h=1e-6):
    x = np.asarray(x, dtype=float)
    n = x.size
    g = np.zeros(n)
    for i in range(n):
        xp = x.copy(); xm = x.copy()
        xp[i] += h
        xm[i] -= h
        g[i] = (f(xp) - f(xm)) / (2.0*h)
    return g

def approx_hess(f, x, h=1e-4):
    x = np.asarray(x, dtype=float)
    n = x.size
    H = np.zeros((n, n))
    fx = f(x)

    # diagonais
    for i in range(n):
        xp = x.copy(); xm = x.copy()
        xp[i] += h
        xm[i] -= h
        H[i, i] = (f(xp) - 2.0*fx + f(xm)) / (h**2)

    # fora da diagonal (mistas)
    for i in range(n):
        for j in range(i+1, n):
            xpp = x.copy(); xpm = x.copy()
            xmp = x.copy(); xmm = x.copy()

            xpp[i] += h; xpp[j] += h
            xpm[i] += h; xpm[j] -= h
            xmp[i] -= h; xmp[j] += h
            xmm[i] -= h; xmm[j] -= h

            Hij = (f(xpp) - f(xpm) - f(xmp) + f(xmm)) / (4.0*h*h)
            H[i, j] = Hij
            H[j, i] = Hij
    return H


# ============================================================
# Busca linear - Backtracking Armijo (Aula 2)
# ============================================================

def backtracking_armijo(f, x, p, g, alpha0=1.0, rho=0.5, c=1e-4, min_alpha=1e-12):
    alpha = alpha0
    fx = f(x)
    gTp = float(np.dot(g, p))
    # Queremos descida: gTp < 0 normalmente (direção de descida)
    while alpha >= min_alpha:
        if f(x + alpha*p) <= fx + c*alpha*gTp:
            return alpha
        alpha *= rho
    return alpha


# ============================================================
# Razão áurea para minimizar phi(alpha) em [a,b] (Aula 2)
# ============================================================

def golden_section_search(phi, a=0.0, b=1.0, tol=1e-5, max_iter=200):
    gr = (np.sqrt(5) - 1) / 2  # ~0.618
    c = b - gr*(b - a)
    d = a + gr*(b - a)
    fc = phi(c)
    fd = phi(d)

    for _ in range(max_iter):
        if abs(b - a) < tol:
            break
        if fc < fd:
            b, d, fd = d, c, fc
            c = b - gr*(b - a)
            fc = phi(c)
        else:
            a, c, fc = c, d, fd
            d = a + gr*(b - a)
            fd = phi(d)
    return 0.5*(a + b)


# ============================================================
# Hessiana "definida positiva": H + lambda I
# ============================================================

def make_pos_def(H, tau=1e-8, max_tries=30):
    H = 0.5*(H + H.T)  # força simetria
    eigs = np.linalg.eigvalsh(H)
    min_eig = float(np.min(eigs))
    if min_eig > 0:
        return H, 0.0

    lam = (-min_eig) + tau
    for _ in range(max_tries):
        Hreg = H + lam*np.eye(H.shape[0])
        if np.min(np.linalg.eigvalsh(Hreg)) > 0:
            return Hreg, lam
        lam *= 10.0
    return H + lam*np.eye(H.shape[0]), lam


# ============================================================
# 1) Gradiente Descendente + Razão Áurea
# x_{k+1} = x_k - alpha_k * g_k
# ============================================================

def grad_desc_golden(f, x0, tol=1e-6, max_iter=2000, h_grad=1e-6, verbose=False):
    x = np.asarray(x0, dtype=float)
    for k in range(1, max_iter+1):
        g = approx_grad(f, x, h=h_grad)
        ng = np.linalg.norm(g)

        if verbose:
            print(f"[GD {k}] f={f(x):.6e} ||g||={ng:.3e} x={x}")

        if ng < tol:
            break

        phi = lambda a: f(x - a*g)
        alpha = golden_section_search(phi, 0.0, 1.0, tol=1e-5, max_iter=200)
        x = x - alpha*g
    return x, k


# ============================================================
# 2) Newton (FD grad/hess + positivação + backtracking)
# resolve H d = -g
# ============================================================

def newton_fd(f, x0, tol=1e-6, max_iter=200, h_grad=1e-6, h_hess=1e-4, verbose=False):
    x = np.asarray(x0, dtype=float)
    for k in range(1, max_iter+1):
        g = approx_grad(f, x, h=h_grad)
        ng = np.linalg.norm(g)

        if verbose:
            print(f"[Newton {k}] f={f(x):.6e} ||g||={ng:.3e} x={x}")

        if ng < tol:
            break

        H = approx_hess(f, x, h=h_hess)
        Hpos, lam = make_pos_def(H)

        # direção de Newton
        try:
            p = -np.linalg.solve(Hpos, g)
        except np.linalg.LinAlgError:
            p = -g  # fallback simples

        alpha = backtracking_armijo(f, x, p, g, alpha0=1.0)
        x = x + alpha*p
    return x, k


# ============================================================
# 3) BFGS (quasi-Newton) + backtracking
# mantém aproximação da inversa da Hessiana: Hk ~ inv(Hess)
# ============================================================

def bfgs_fd(f, x0, tol=1e-6, max_iter=1000, h_grad=1e-6, verbose=False):
    x = np.asarray(x0, dtype=float)
    n = x.size
    Hk = np.eye(n)

    g = approx_grad(f, x, h=h_grad)

    for k in range(1, max_iter+1):
        ng = np.linalg.norm(g)

        if verbose:
            print(f"[BFGS {k}] f={f(x):.6e} ||g||={ng:.3e} x={x}")

        if ng < tol:
            break

        p = -Hk @ g
        alpha = backtracking_armijo(f, x, p, g, alpha0=1.0)
        s = alpha*p
        x_new = x + s
        g_new = approx_grad(f, x_new, h=h_grad)

        y = g_new - g
        ys = float(np.dot(y, s))

        # Atualização BFGS padrão (só se condição numérica ok)
        if ys > 1e-12:
            rho = 1.0 / ys
            I = np.eye(n)
            V = I - rho * np.outer(s, y)
            Hk = V @ Hk @ V.T + rho * np.outer(s, s)

        x, g = x_new, g_new

    return x, k


# ============================================================
# Execução / Comparação
# ============================================================

def summarize(name, x):
    x_star = np.ones(3)
    fx = rosenbrock3(x)
    gnorm = np.linalg.norm(approx_grad(rosenbrock3, x))
    dist = np.linalg.norm(x - x_star)
    print(f"\n== {name} ==")
    print("x_final =", x)
    print("f(x_final) =", fx)
    print("||grad|| ~", gnorm)
    print("dist até (1,1,1) =", dist)

if __name__ == "__main__":
    # ponto inicial clássico "difícil" pro Rosenbrock:
    x0 = np.array([-1.2, 1.0, 1.0])

    x_gd, it_gd = grad_desc_golden(rosenbrock3, x0, verbose=False)
    summarize(f"Gradiente + Razão Áurea (it={it_gd})", x_gd)

    x_nt, it_nt = newton_fd(rosenbrock3, x0, verbose=False)
    summarize(f"Newton FD + Hessiana PD + Armijo (it={it_nt})", x_nt)

    x_bf, it_bf = bfgs_fd(rosenbrock3, x0, verbose=False)
    summarize(f"BFGS FD + Armijo (it={it_bf})", x_bf)

    # (opcional) testar influência de h no Newton:
    # for hg, hh in [(1e-4,1e-2),(1e-6,1e-4),(1e-8,1e-6)]:
    #     x_nt2, it_nt2 = newton_fd(rosenbrock3, x0, h_grad=hg, h_hess=hh, verbose=False)
    #     print(f"\nNewton com h_grad={hg}, h_hess={hh} -> it={it_nt2}, f={rosenbrock3(x_nt2):.3e}, x={x_nt2}")
```