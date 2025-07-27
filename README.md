# Fine-Tuning-M2M100-on-Nepali
Breaking the Language Barrier: Fine-Tuning M2M100 for English to Nepali Translation

This project fine-tunes Meta's multilingual machine translation model [`facebook/m2m100_418M`] on an English-to-Nepali dataset to improve performance on low-resource translation tasks.

##  Objective

To adapt the pretrained `m2m100_418M` model specifically for **English ⇄ Nepali** translation using supervised fine-tuning and evaluate performance using BLEU, SacreBLEU, and BERTScore metrics.

---

## Dataset

- **Name:** [`CohleM/english-to-nepali`](https://huggingface.co/datasets/CohleM/english-to-nepali)
- **Source:** Hugging Face Datasets Hub
- **Languages:** English (`en`) → Nepali (`ne`)
- **Format:** JSON format with `"translation"` field containing both `"en"` and `"ne"` keys

---

## Model

- Base model: [`facebook/m2m100_418M`](https://huggingface.co/facebook/m2m100_418M)
- Type: Sequence-to-sequence Transformer
- Tokenizer: `M2M100Tokenizer`

---

## Hyperparameters for Fine-Tuning

| Hyperparameter           | Value                  |
|--------------------------|------------------------|
| Model                    | facebook/m2m100_418M   |
| Batch size per device    | 8                      |
| Optimizer                | AdamW                  |
| Learning rate            | 2e-5                   |
| Epochs                   | 1                      |
| Total training steps     | `len(train_dataloader) * 1` |
| Learning rate scheduler  | Linear                 |
| Device                   | CUDA if available      |



## Example Translations

### Without Fine-Tuning

#### Easy
- **English:** My name is Gyawali.  
- **Nepali (Predicted):** मेरो नाम जियावाली हो ।

#### Medium
- **English:** She likes to read books in the evening after finishing her homework.  
- **Nepali (Predicted):** घरबेटीले जहाँ पायो त्यहाँ पकाउन दिँदैन ।

#### Hard
- **English:** Despite the economic challenges, the government is planning to invest more in renewable energy sources to ensure a sustainable future.  
- **Nepali (Predicted):** नयाँ संविधानको घोषणा, आन्दोलनको निराशाजनक बैठान, तीनै तहको निर्वाचन पश्चातको देश र मधेसको स्थितिको वास्तविक विश्लेषण हुनु आवश्यक छ ।

---

## After Fine-Tuning

### Easy
- **English:** My name is Gyawali.  
- **Predicted Nepali:** मेरो नाम गिवाली हो।


---

###  Medium 
- **English:** he likes to read books in the evening after finishing her homework.  
- **Predicted Nepali:** उनी आफ्नो गृह कार्य समाप्त भएपछि साँझमा किताब पढ्न मन पराउँछन्।


---

###  Hard
- **English:** Despite the economic challenges, the government is planning to invest more in renewable energy sources to ensure a sustainable future.  
- **Predicted Nepali:** आर्थिक चुनौतिका बाबजुद सरकारले दिगो भविष्यलाई सुनिश्चित गर्न नवीकरणीय ऊर्जाको स्रोतमा बढी लगानी गर्ने योजना रहेको छ।


---
## Evaluation Metrics

| Difficulty | BLEU (NLTK) | SacreBLEU | BERTScore F1 | Notes |
|------------|-------------|-----------|---------------|-------|
| Easy       | 0.1862      | 35.36     | 0.8944        | Minor spelling error |
| Medium     | 0.1161      | 13.95     | 0.8889        | Formal paraphrasing |
| Hard       | 0.1441      | 16.61     | 0.9069        | Great semantic accuracy |

- **BLEU**: Penalizes rephrasing and grammar differences
- **SacreBLEU**: Better standardized BLEU variant
- **BERTScore**: High semantic similarity indicates good translation quality

---

## Conclusion

- The base model (`facebook/m2m100_418M`) struggled with accurate translation before fine-tuning, especially in medium and hard cases.
- After fine-tuning:
  **Semantic accuracy** (BERTScore) improved significantly across all difficulty levels.
  **Lexical accuracy** (BLEU, SacreBLEU) improved, though remained relatively low due to paraphrasing and stylistic changes.
- This suggests the model is **learning meaningful translation patterns**, even if exact phrasing differs.

