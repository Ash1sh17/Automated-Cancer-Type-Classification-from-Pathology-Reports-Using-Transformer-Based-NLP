Automated Cancer Type Classification from Pathology Reports

Using Transformer-Based NLP | CSC 590 | CSUDH

Srinivas Ashish Maddula | GitHub: github.com/Ash1sh17
	
Project Overview: 

This project uses natural language processing to automatically classify cancer types from free-text clinical pathology reports. Using 9,522 reports from The Cancer Genome Atlas (TCGA) spanning 32 distinct cancer types, four models were built and evaluated: Random Forest, Linear SVM, Google BERT, and PubMedBERT.

The preprocessing pipeline lowercases all text, removes non-alphabetic characters, strips common English stop words, and drops tokens of two characters or fewer  reducing each report from roughly 80,000 raw tokens to around 15,000 meaningful medical terms. For the classical models, these cleaned tokens are converted to numerical features using TF-IDF vectorization with 15,000 features, unigrams plus bigrams, and sublinear TF scaling. For the transformer models, the text is tokenized using each model's native tokenizer with a maximum sequence length of 256 tokens.

The dataset was split 80/20 into training (7,617 samples) and test (1,905 samples) using stratified sampling so that all 32 cancer types appear in both sets, even the rarest ones. All four models were trained and evaluated on the same split under identical conditions for a fair comparison.

The best result came from Linear SVM at 97.7% accuracy and 97.6% weighted F1 outperforming both BERT models. PubMedBERT reached 97.1% accuracy, beating general BERT at 95.7%, confirming that domain-specific pre-training on biomedical text provides a real advantage. Confusion matrix analysis showed that errors cluster between biologically similar subtypes such as KIRC and KIRP (kidney), COAD and READ (colorectal), and LUAD and LUSC (lung) the same pairs that human pathologists sometimes disagree on.

Steps to Execute in VS Code:

1.  Clone the Repository
Open the VS Code terminal using Cmd + backtick (or go to Terminal > New Terminal) and run:

git clone https://github.com/Ash1sh17/Automated-Cancer-Type-Cl....git
cd Automated-Cancer-Type-Classification

2.  Create and Activate a Virtual Environment

python -m venv venv

# Mac / Linux
source venv/bin/activate

# Windows
venv\Scripts\activate

3.  Install Required Packages

pip install numpy pandas matplotlib seaborn scikit-learn nltk
pip install torch transformers datasets accelerate

Mac note: On Apple Silicon (M1/M2/M3), PyTorch automatically uses the MPS backend for GPU acceleration. No CUDA setup needed. Training BERT and PubMedBERT takes approximately 2 to 4 hours per model on MPS. On older Intel Macs, training runs on CPU and may take 6 to 10 hours per model.

4.  Open the Notebook

In VS Code go to File, then Open File, and select Finalized_project_5epochs.ipynb. In the top-right corner click Select Kernel and choose the venv Python environment you just created.

5.  Run the Notebook Cells in Order

The notebook has 26 steps. Run them from top to bottom using Shift + Enter on each cell, or click Run All from the toolbar. The key sections are:

Cells 1–3: imports and environment setup
Cells 4–6: automatically downloads the TCGA dataset from GitHub
Cells 7–10: loads the data and shows the cancer type distribution chart
Cells 11–18: text cleaning and TF-IDF vectorization
Cells 19–24: trains Random Forest and Linear SVM, prints results and confusion matrices
Cells 25–44: tokenizes data and fine-tunes Google BERT then PubMedBERT for 5 epochs each allow             35 to 60 minutes per model on a GPU, or several hours on CPU
Cells 45–50: generates the final comparison chart and all four confusion matrices
Cell 52: live prediction demo picks a random test report and shows the SVM prediction
Cell 54: prints the final conclusion summary

6.  Quick Demo Without GPU

If you only want to see a live prediction without running the BERT models, run cells 1 through 22 to set up the environment, clean the data, and train the SVM, this takes under five minutes on any machine. Then skip directly to cell 52 for the live prediction demo.

Files in This Repository

Finalized_project_5epochs.ipynb - the complete notebook with all outputs already run
Cancer types.png - bar chart of all 32 TCGA cancer types by sample count
Classical Models Confusion Matrix.png - confusion matrices for Random Forest and Linear SVM
Transformers models Confusion Matrix.png - confusion matrices for Google BERT and PubMedBERT
Model comparison.png - accuracy, weighted F1, and evaluation loss charts for all four models
README.md - project description and execution instructions
