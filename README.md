# 🦠 Emergent Molecular Communication

A preliminary study of emergent molecular communication protocols learned by graph-based agents in a diffusion channel environment.

## 📋 Table of Contents

- [🦠 Emergent Molecular Communication](#-emergent-molecular-communication)
  - [📋 Table of Contents](#-table-of-contents)
  - [✏️ Abstract](#️-abstract)
  - [✉️ Authors](#️-authors)
  - [🚀 Usage](#-usage)

---

## ✏️ Abstract

Biological organisms have developed sophisticated communication mechanisms to enhance their adaptability and survival, ranging from molecular signaling to complex linguistic structures. Understanding the evolution of these mechanisms can provide insights into both biological processes and artificial communication system design. As a first attempt in this direction, a preliminary system based on Graph Neural Networks (GNNs) and molecular diffusion models is presented in this paper to observe the emergence of Molecular Communication (MC) protocols among artificial agents. In particular, these agents interact according to a Lewis-game framework by exchanging molecules that diffuse in a fluidic environment. In this framework, a sender encodes and transmits symbols to a destination with the help of intermediate relay nodes, subject to the stochastic behavior of diffusion-based MC, which affects message integrity. Each of these nodes can tune its internal parameters to influence communication, mimicking the evolution of biological organisms such as bacteria. Preliminary numerical results suggest that this system can learn to evolve an effective MC protocol. The findings highlight the potential of such a system for investigating emergent MC, possibly leading to a better understanding of molecular biological systems and the optimization of bio-based and bio-inspired networked systems.

## ✉️ Authors

- **Alberto Archetti**<sup>1</sup>  
- **Gabriele Giusti**<sup>1</sup>  
- **Karthik R. Gorla**<sup>1,3</sup>  
- **Stefano Caputo**<sup>2</sup>  
- **Maurizio Magarini**<sup>1</sup>  
- **Matteo Matteucci**<sup>1</sup>  
- **Lorenzo Mucchi**<sup>2</sup>  
- **Massimiliano Pierobon**<sup>3</sup>  

<sup>1</sup>Department of Electronics, Information, and Bioengineering, Politecnico di Milano, Milan, Italy  
<sup>2</sup>Department of Information Engineering, Università degli Studi di Firenze, Florence, Italy  
<sup>3</sup>School of Computing, University of Nebraska–Lincoln, Lincoln, NE, USA

## ⚙️ Installation
1. Clone the repo
```bash
git clone https://github.com/<OWNER>/<REPO>.git
cd <REPO>
```
2. Create Conda environment
```bash
conda env create -f environment.yml
conda activate commence
```
3. Install Python dependencies
```bash
poetry install
```

## 🚀 Usage
Run the Jupyter notebook to train, evaluate, and collect metrics:
```bash
jupyter lab commence_model.ipynb
```
