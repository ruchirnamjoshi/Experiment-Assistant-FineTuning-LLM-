# 🧪 BioMistral Wet-Lab Protocol Assistant  
*Fine-tuning Large Language Models for Structured Experimental Design*

---

## 📌 Project Overview  

This project demonstrates how **domain-specific fine-tuning** of a large language model can significantly improve its ability to **generate structured, reproducible wet-lab protocols** for biological research.  

We start from the open-source **[BioMistral-7B](https://huggingface.co/BioMistral/BioMistral-7B)** model (a biomedical specialization of Mistral), fine-tune it on the **BioProBench** dataset, and deploy an interactive **Gradio app** that helps researchers design experiments in a structured, conversational way.

🔗 **Live Demo**: https://drive.google.com/file/d/1ui6vkc21LYfL7yrNqB8TpmrjkLLDDepR/view?usp=sharing  

---

## 🚀 Key Features  

- **Fine-tuned Biomedical LLM**:  
  Adapted BioMistral-7B using parameter-efficient fine-tuning (LoRA/QLoRA).  

- **Structured Protocol Generation**:  
  Model outputs protocols with sections like **Title, Objective, Materials, Safety, Procedure, QC, Troubleshooting, Notes**.  

- **Gradio App with Conversational Flow**:  
  - Text & speech input (ASR)  
  - Streaming protocol generation (outputs appear step-by-step)  
  - Variant comparison (two protocols with different decoding configs)  
  - Export as **PDF** (well-formatted with sections & conversation history)  

- **Audio Narration (planned)**:  
  Converts protocol into a concise spoken narration for accessibility and lab convenience.  
 

---

## 🧠 Motivation & Use Case  

🔬 **Problem**:  
Designing reproducible experimental protocols in biology is **time-consuming and error-prone**. Researchers often struggle with:  
- Incomplete documentation of steps  
- Lack of standardization across labs  
- Accessibility (especially for non-native English speakers or visually impaired users)  

💡 **My Solution**:  
- Use an LLM fine-tuned on biomedical tasks to **automatically draft structured, standardized wet-lab protocols**.  
- Provide **interactive refinements** via a conversational Gradio UI.  
- Enable **variant comparison** so researchers can evaluate alternatives.  
- Support **multimodal interaction** (speech input/output).  

✅ This bridges the gap between **scientific knowledge** and **practical lab execution**.  

---

## 🛠️ Technical Workflow  

### 1. Data Preparation  
- Dataset: [BioProBench](https://huggingface.co/datasets/BioProBench/BioProBench)  
- Extracted JSON files for training/testing  
- Normalized into fields: `system_prompt`, `instruction`, `input`, `output`, `id`, `type`

### 2. Fine-Tuning  
- **Base Model**: `BioMistral/BioMistral-7B`  
- **Technique**: QLoRA (4-bit quantization + LoRA adapters)  
- **Training Setup**:  
  - Trained on Colab A100  
  - ~1.1% of parameters trainable (~42M params)  
  - Used Hugging Face `Trainer` with PEFT  
- **Artifacts**: Model adapters pushed to Hugging Face Hub  

### 3. Evaluation  
- Measured with **ROUGE-L** on held-out protocols  
- Conducted manual inspection → outputs show improved structure & biomedical context  

### 4. Gradio App  
- Built with **Gradio Blocks**  
- Supports:  
  - Text & speech input  
  - Streaming generation  
  - Compare two variants (different decoding settings)  
  - Save as **PDF** (conversation + protocol)  
- Backend integrates Hugging Face model + PEFT adapters  

### 5. Deployment  
- Packaged and deployed on **Hugging Face Spaces**  
- Private adapter repo loading with token auth, or merged full model for public demo  

---

## 📊 Results  

- **Before fine-tuning**: Model outputs generic, sometimes irrelevant responses.  
- **After fine-tuning**:  
  - Structured protocols with clear sections  
  - Better biomedical terminology usage  
  - Fewer hallucinations compared to base BioMistral  

 ---

## 🌟 Why This Project is Unique  

- **Domain-specialized**: Not just a generic chatbot, but fine-tuned for **lab protocols**.  
- **Parameter-efficient training**: Achieves strong results with only ~1% of weights updated.  
- **Human-friendly interaction**: Speech input/output + structured PDFs.  
- **Practical impact**: Can accelerate research reproducibility, aid teaching, and assist labs with limited resources.  
