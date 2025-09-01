# 🚀 Google Summer of Code 2025 - Final Report  
## Highly Granular Quantization for CICADA  

### 📌 Project Info  

| **Contributor** | Abhishikth Mallampalli |
|:-----------------|:-------------------------|
| **Mentor(s)**   | Lino Gerlach, Isobel Ojalvo, Jennifer Ngadiuba |
| **Organization** | CERN-HSF, Princeton University |
| **Project Link** | [GSoC Project Page](https://summerofcode.withgoogle.com/programs/2025/projects/b1JQ9zmB) |
| **Project Webpage** | [CICADA](https://cicada.web.cern.ch/) |
| **Base Repo** | [Princeton-AD/cicada](https://github.com/Princeton-AD/cicada) |

---

## 📖 1. Project Overview  

<p align="justify">
The <b>CICADA (Calorimeter Image Convolutional Anomaly Detection Algorithm)</b> project aims to detect anomalous physics signatures without bias from theoretical models in proton–proton collisions at the Compact Muon Solenoid (CMS) experiment at the Large Hadron Collider. CICADA identifies anomalies in low-level calorimeter trigger data using a <b>convolutional autoencoder</b>, whose behavior is transferred to compact student models via <b>knowledge distillation</b>. Careful model design and quantization ensure <b>sub-200 ns</b> inference times on <b>Field Programmable Gate Arrays (FPGAs)</b>.
</p>

<p align="justify">
CICADA currently uses a distilled neural network model with layer-wise quantization to meet the strict sub-200ns latency required for the CMS Level-1 Trigger (L1T), trained using <b>QKeras</b> (a now-deprecated library for quantization-aware training). This GSoC project enhanced CICADA by integrating <b>highly granular quantization (HGQ)</b> techniques, which allow automatic, per-weight and per-bias quantization, providing finer control over model precision and resource usage. I developed a HGQ version of the CICADA distilled model and evaluated its performance and resource consumption on an FPGA, while contributing to the open-source CICADA, HGQ2, and hls4ml frameworks as needed. Notably, the HGQ2 library is compatible with <b>JAX</b>, opening the door for future integration with modern, hardware-friendly ML ecosystems.
</p>

---

## 🛠️ 2. Work Done Over the Summer  

- ⚡ **CICADA Input Data Workflow**  
  <details>
  <summary>Details</summary>  

  - Designed the CICADA input data generation workflow to be able to use CMS open data, using containers, and creating a public GitHub repo → [Repo](https://github.com/abhi-mal/cicada_inputs).  
  - This enables wider reach, reproducibility, and further community-driven research.  Verified that the new workflow reproduces the current CICADA performance when using the same inputs. 


  </details>

- 🧪 **Alternative Training Strategies**  
  <details>
  <summary>Details</summary>  

  - Investigated alternative training strategies for CICADA, particularly different ways of outlier exposure.  
  - Added functionality to generate synthetic anomaly data from noise.  
  - Showed how various outlier generation strategies have their own quirks and tradeoffs. 
  - Motivation: move toward fully unsupervised training, eliminating the need for signal MC simulations.  

  </details>

- 🐞 **Bug Fixes & Updates**  
  <details>
  <summary>Details</summary>  

  - Updated scripts to work with latest package versions.  
  - Fixed bugs including memory leak issues that caused GPU training crashes.  

  </details>

- 🔧 **HGQ Student Models**  
  <details>
  <summary>Details</summary>  

  - Developed HGQ student models → [Fork](https://github.com/abhi-mal/cicada/tree/hgq2), [PR](https://github.com/Princeton-AD/cicada/pull/17).  
  - Designed evaluation pipeline to study performance vs. resource tradeoffs.  

  </details>

- 🛠️ **hls4ml Bug Fix**  
  <details>
  <summary>Details</summary>  

  - Found and reported a bug in the **hls4ml** library when using HGQ → [Issue](https://github.com/fastmachinelearning/hls4ml/issues/1364).  
  - Proposed a fix → [PR](https://github.com/fastmachinelearning/hls4ml/pull/1365).  
  - Developers later implemented an official solution.  

  </details>

- ⚙️ **FPGA Evaluation Workflow**  
  <details>
  <summary>Details</summary>  

  - The existing synthesis evaluation workflow used internal CMSSW software → [Tool](https://github.com/pallabidas/L1TRegionDumper).  
  - Designed an alternative faster workflow to test new models.  
  - Verified that HGQ student models are indeed performing as desired.  

  </details>

- 📊 **New Input Variable Study**  
  <details>
  <summary>Details</summary>  

  - Analyzed the potential of incorporating new input variables to enhance the model's awareness.
  - The study concluded that these variables are physically significant and add valuable, non-redundant information compared to the existing inputs. 

  </details>

- 🔍 **Student Model Evaluation Pipeline**  
  <details>
  <summary>Details</summary>  

  - Developed evaluation pipeline to study tradeoffs in performance of various student models.
  - This pipeline has already been used to study various HGQ models and another promising quantization technique, Logic Gate Networks, and can be used to test future quantization libraries.

  </details>

- 📄 **Papers**  
  <details open>
  <summary>Details</summary>  

  - Submitted a paper based on this project to a machine learning workshop.  
  - Will also be presenting results at **FastML 2025 in Zurich** → [Indico Link](https://indico.cern.ch/event/1496673/contributions/6637975/).  

  </details>
  

- 🚀 **Final HGQ Model**  
  <details open>
  <summary>Details</summary>  

  - Achieved ~**2× lower latency** and ~**6× lower FPGA resource usage** (Vitis HLS estimates).  
  - HGQ library suggests further reductions can be expected after place-and-route.  

  </details>


---

## 📎 Links  

<details>
<summary>Click to expand</summary>

1. [CICADA Input Workflow](https://github.com/abhi-mal/cicada_inputs)  
2. [HGQ Student Models](https://github.com/abhi-mal/cicada/tree/hgq2)  
3. [hls4ml Issue #1364](https://github.com/fastmachinelearning/hls4ml/issues/1364)  
4. [hls4ml PR #1365](https://github.com/fastmachinelearning/hls4ml/pull/1365)  
5. [CMSSW Dumper Tool](https://github.com/pallabidas/L1TRegionDumper)  
6. [FastML 2025 Workshop](https://indico.cern.ch/event/1496673/)  

</details>

## 📚 3. Learnings  

<p align="justify">

Gained experience in:

 - Deploying models in resource-constrained, low-latency environments
 - Synthetic data generation
 - Debugging FPGA synthesis and evaluating quantization tradeoffs  
 - Designing evaluation pipelines and assessing model performance  
 - Managing multiple aspects of a complex project simultaneously  
 - Writing reusable and maintainable code  

These experiences strengthened both my technical skills and collaborative problem-solving abilities.

</p>

---

## 🔮 4. Future Work  

<details>
<summary>Click to expand</summary>

- Investigate if training can be improved by including student feedback to the teacher.
- Perform full **place-and-route** and check the HGQ library claim of further drop in resources.
- Further explore **outlier exposure** training methods.  
- The reduced resource usage opens the possibility of exploring more advanced student models that incorporate the additional input variables studied this summer. These variables were shown to be physically significant, but are not included in the current QKeras-based CICADA student model.

</details>

---

## 🙏 Thank You!  

<p align="justify">
Thanks to my mentors for giving me the opportunity to work on such an exciting project. Special thanks to Lino and Isobel for their guidance, enthusiastic discussions, and incredible support. This has been an amazing learning experience.
</p>
