# CodeAlpha_Data-Analytics3
# TASK 4: Sentiment Analysis
import pandas as pd
import os

# A simple Rule-Based NLP Lexicon function to detect emotion/sentiment
def get_sentiment(text):
    text = text.lower()
    positive_words = ['awesome', 'love', 'comfortable', 'perfectly', 'excellent', 'amazing', 'recommended', 'good']
    negative_words = ['disappointed', 'damaged', 'waste', 'worst', 'boring', 'bad', 'faded', 'terrible', 'defective']
    
    pos_count = sum(1 for word in positive_words if word in text)
    neg_count = sum(1 for word in negative_words if word in text)
    
    if pos_count > neg_count:
        return 'Positive'
    elif neg_count > pos_count:
        return 'Negative'
    else:
        return 'Neutral'

def analyze_sentiment():
    print("--- Starting Task 4: Sentiment Analysis ---")
    
    if not os.path.exists("amazon_reviews.csv"):
        print("Error: 'amazon_reviews.csv' not found. Please run task2_eda.py first!")
        return
        
    df = pd.read_csv("amazon_reviews.csv")
    
    # Applying NLP classification function to text column
    df['Sentiment'] = df['Review_Text'].apply(get_sentiment)
    
    print("\n--- Sentiment Analysis Results ---")
    print(df[['Review_Text', 'Sentiment']])
    
    print("\n--- Sentiment Overview Counts ---")
    print(df['Sentiment'].value_counts())
    
    # Save the final insights
    df.to_csv("analyzed_sentiment_output.csv", index=False)
    print("\nTask 4 Complete! Results saved to 'analyzed_sentiment_output.csv'")

if _name_ == "_main_":
    analyze_sentiment()
