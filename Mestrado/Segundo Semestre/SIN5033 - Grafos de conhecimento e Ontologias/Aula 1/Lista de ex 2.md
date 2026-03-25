# Lista de ex. 2:
https://edisciplinas.usp.br/pluginfile.php/9501669/mod_resource/content/1/Exerc%C3%ADciosLogicaDs.pdf

---

1. Conceitos de linguagem natural para conceitos ALC:

**i.** Pessoa feliz:
$$\text{Pessoa} \sqcap \text{Feliz}$$

**ii.** Pessoa feliz dona de pet: 
$$\text{Pessoa} \sqcap \text{Feliz} \sqcap \exists \text{donoDe.Animal}$$

**iii.** Pessoa que é dona só de gatos: 
$$\text{Pessoa} \sqcap \forall\text{donoDe.Gato}$$

**iv.** Pesosa que não é feliz, é dona de pet, e que tem um gato velho:
$$\text{Pessoa} \sqcap \neg \text{Feliz} \sqcap \exists \text{donoDe.}(\text{Animal} \sqcap \text{Gato} \sqcap \text{Velho})$$

**v.** Pessoa que é dona só de gatos ou peixes 
$$\text{Pessoa} \sqcap \exists \text{donoDe.Animal} \sqcap \forall \text{donoDe.(Gato} \sqcup \text{Peixe} \text{)}$$

---





2. 
**i.** *Carros são exatamente aqueles veículos que têm rodas e são movidos por um motor:*
$$
\text{Carros} \equiv \text{Veículo} \sqcap \exists \text{temParte.Roda} \sqcap \exists \text{movidoPor.Motor}
$$

**ii.** *As bicicletas são exatamente aqueles veículos que têm rodas e são movidos por um ser humano:*

$$
\text{Bicicletas} \equiv \text{Veículo} \sqcap \exists \text{temParte.Roda} \sqcap \exists \text{movidoPor.SerHumano}
$$

**iii.** *Os barcos são exatamente aqueles veículos que viajam na água.*
$$
\text{Barcos} \equiv \text{Veículo} \sqcap \exists \text{viajamNa.Água}
$$

**iv.** *Os barcos não têm rodas.*
$$
\text{Barcos} \sqsubseteq \forall \text{temParte.} \neg \text{Roda}
$$

**v.** *Carros e bicicletas não viajam na água.*
$$
\text{Carros} \sqcup \text{Bicicletas} \sqsubseteq \text{viajamNa.} \neg \text{Água}
$$

**vi.** *Rodas são exatamente aqueles dispositivos que possuem um eixo e podem girar*
$$
\text{Roda} \equiv \text{Dispositivo} \sqsubseteq \text{temParte.Eixo} \text{WIP}
$$

3. Qual dos seguintes conceitos é satisfatório?
**i.** $A \sqcap \neg A$
**ii.**
**iii.**
**iv.**
