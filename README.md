# Sentiment-Analysis-balé-by-btn

🏦 This project performs sentiment analysis on user reviews of the *balé by BTN* application, scraped from *Google Play Store*. The model used is **IndoBERT** (`indobenchmark/indobert-base-p1`), a pre-trained language model specifically designed for Indonesian. It was _fine-tuned_ on the review dataset to generate relevant sentiment predictions and identify dominant words frequently used in both positive and negative reviews.

## Features
- `reviewId`: unique id for each review.
- `userName`: name of the user who submitted the review.
- `userImage`: URL of the user's profile image.
- `content`: the review text written by the user.
- `score`: rating given by the user (1-5).
- `thumbsUpCount`: number of likes received from other users.
- `reviewCreatedVersion`: app version at the time of review.
- `at`: date and time when the review was submitted.
- `replyContent`: developer's response to the review.
- `repliedAt`: date and time of the developer's reply.

## Methodology
### Data Scraping
The dataset consists of the latest **2,500 reviews** scraped from Google Play Store using `google_play_scraper`. Only reviews written in Indonesian and submitted between **October 2024 and April 2025** were included.
Sentiment labels (positive or negative) were **manually assigned** based on the corresponding rating scores.
- 1-3 → negative.
- 4-5 → positive.

### Data Preprocessing
1. **Case-folding**: Converting all characters in the reviews to lowercase.
2. **Data Cleaning**: Removing non-letter characters, such as numbers, punctuation, excessive whitespace, or other symbols that are less relevant for text analysis, as well as handling missing values and duplicate entries.
3. **Text Normalization**: Using a standardized dictionary, namely Kamus Alay (Colloquial Indonesian Lexicon), to normalize words into their standard forms.
4. **Filtering**: Removing stopwords to retain only meaningful terms.

In this project, **three** different types of data preprocessing were applied.
1. **Full preprocessing**: Using all the preprocessing steps mentioned above, resulting in a total of 2,280 remaining reviews for further analysis.
2. **Full preprocessing + custom stopwords**: Using all steps, with additional stopwords: aplikasi, aplikasinya, apk, bank, btn, bale, banget, kali, mobile, ya. This process left 2,347 reviews for further analysis.
3. **Partial preprocessing**: Omitting case-folding and filtering, also left a total of 2,347 remaining reviews.

### Exploratory Data Analysis
This step uses dataset preprocessed with type 2, which applied more contextually appropriate stopword cleaning than types 1 and 3.
- **Word Clouds**: Visualized frequent words in positive and negative reviews.
- **Pie Chart**: Displayed proportion of positive and negative sentiments.

### Modelling
Consists of **four** main steps:
1. **Splitting Data**
   - Training (70%)
   - Validation (15%)
   - Testing (15%)
2. **Tokenization**: Splitting the review into tokens using IndoBERT Tokenizer.
3. **Dataset Preparation**: Converting the tokenized results into the format required for model training.
4. **Training**: Defining hyperparameters such as the number of epochs, batch size, learning rate, etc.

**Four** different models were trained:
1. Using the dataset with preprocessing type 1.
2. Using the dataset with preprocessing type 3, trained for 5 epochs.
3. Using the dataset with preprocessing type 3, trained for 7 epochs.
4. Using the dataset with preprocessing type 2.

### Evaluation
- Precision
- Recall
- F1-Score
- Accuracy

## Conclusion
- User sentiment toward the balé by BTN application appeared **fairly balanced**.
- **Negative reviews** reflected user complaints about technical issues during usage, while **positive reviews** highlighted satisfaction with the app’s ease of use and usefulness.
- **IndoBERT effectively captured** sentiment in Indonesian, with all four models **achieving** over 91% accuracy and high precision, recall, and F1-scores.
- **Model 2** is the best model, reaching 95% **accuracy** and an **F1-Score** of 0.95–0.96.
