# UIUC-CS410-Project


Best Price Flight Recommender Project Proposal and Progress Report

Project Description

The Best Price Flight Recommender project aims to create a user-friendly platform that retrieves and analyzes flight data from Expedia, delivering personalized flight recommendations to users based on their preferences. By leveraging web scraping, data processing, and machine learning through OpenAI, this system will help travelers find the best flights according to factors like budget, duration, and airlines.

Project Components

1. Web Crawler

The project requires a web crawler to fetch flight data from Expedia. We’ll use Python libraries like BeautifulSoup and requests to retrieve static flight details, while Selenium will be utilized to handle dynamic content. The crawler will collect essential flight information, such as flight schedules, airlines, layovers, and prices, structuring the data for further processing.

Sample Code for Web Crawler:

import requests from bs4 import BeautifulSoup

def fetch_flight_data(url): response = requests.get(url) if response.status_code == 200: soup = BeautifulSoup(response.content, "html.parser") # Extraction logic for flight details return flight_data return None

2. Data Processing

The data collected by the crawler requires cleaning and standardization. This step involves removing irrelevant elements, handling missing values, and standardizing price formats, timestamps, and other critical fields for consistency. Data is processed using Pandas to prepare it for recommendation filtering.

Sample Code for Data Cleaning:

import pandas as pd

def clean_flight_data(raw_data): df = pd.DataFrame(raw_data) # Example of cleaning and formatting steps df['price'] = df['price'].apply(lambda x: float(x.replace('$', ''))) return df

3. Integration with OpenAI

With cleaned and standardized flight data, the next step is integrating OpenAI’s model to generate recommendations based on user preferences. Models like GPT-4 or Davinci can be prompted to filter options and provide insights, considering parameters like shortest duration, budget, or specific airlines. Using OpenAI's API, we can fine-tune prompts to ensure relevant recommendations.

Sample Code for OpenAI Integration:

import openai

def get_recommendations(prompt): openai.api_key = "YOUR_API_KEY" response = openai.Completion.create( model="gpt-4", prompt=prompt, max_tokens=150 ) return response.choices[0].text.strip()

4. Recommendation Engine

The recommendation engine uses the OpenAI output to select flights based on factors such as layover times, departure and arrival times, and pricing. It can also suggest alternate flights from nearby airports or at different times to find better pricing. This engine will be flexible, adjusting to user preferences dynamically.

Sample Code for Recommendation Filtering:

def filter_recommendations(flight_data, budget=None, max_duration=None): # Filtering logic based on budget and duration filtered_flights = [ flight for flight in flight_data if (budget is None or flight['price'] <= budget) and (max_duration is None or flight['duration'] <= max_duration) ] return filtered_flights

5. User Interface

To create a seamless experience, a web-based user interface will be developed using Flask or Streamlit. This interface will allow users to input their travel details and preferences, such as dates, destinations, and budget constraints. The UI will display the best recommendations tailored to each user's input.

Sample Code for User Interface with Flask:

from flask import Flask, render_template, request

app = Flask(name)

@app.route('/', methods=['GET', 'POST']) def home(): if request.method == 'POST': # Handle user input and display recommendations pass return render_template('index.html')

if name == 'main': app.run(debug=True)

Workflow Summary

User Input: Users enter travel details like destination, dates, and preferences.
Web Crawler: Fetches flight data from Expedia.
Data Processing: Cleans and formats the scraped data.
OpenAI Analysis: Generates personalized flight recommendations.
Recommendation Engine: Filters based on user preferences.
User Interface: Displays the top recommended flights.
Progress Report

1. Progress Made Thus Far

Web Crawler Development: A functional prototype of the web crawler has been implemented, and initial data has been successfully scraped from Expedia. The crawler uses BeautifulSoup to extract structured data, such as flight times, prices, and airlines.

Data Cleaning and Processing: Preliminary data processing steps are completed. Initial scripts for data cleaning using Pandas have been developed to handle missing values, format standardization, and data type conversions.

OpenAI Integration Setup: The OpenAI API integration is partially completed. A basic prompt structure has been designed, and initial tests using GPT-4 have shown promising results in generating recommendations based on cleaned flight data.

User Interface Design: Basic mockups for the UI have been created. The interface design prioritizes ease of use, allowing users to easily input travel information and view recommendations.

2. Remaining Tasks

Refinement of Web Crawler: The crawler requires enhancements to handle more dynamic pages on Expedia. Implementing Selenium to automate interactions with JavaScript-based elements will allow us to access more comprehensive flight data.

Advanced Data Processing: Further data processing is needed to account for edge cases, such as fluctuating prices and limited data availability on certain flights. A method for handling these variations is planned to ensure data accuracy.

Prompt Engineering for OpenAI: While the OpenAI model currently provides basic recommendations, refining prompt structures and experimenting with different models （like GPT-4 and Davinci） will improve the quality and relevance of the recommendations.

Completion of Recommendation Engine: The filtering logic requires additional work to account for flexible user preferences. Features like alternative airport suggestions and optimal layover times need to be fine-tuned.

Development of User Interface: The UI’s core structure is in place, but additional development is needed to ensure a smooth and visually appealing user experience. Integrating the UI with backend services (data fetching, OpenAI recommendations) is also pending.

3. Challenges/Issues Being Faced

Dynamic Content Handling: The primary challenge is handling Expedia’s dynamic content, as some flight data only loads through JavaScript. Although Selenium has been helpful, performance and reliability issues arise when simulating multiple user interactions.

Data Quality and Consistency: Maintaining consistent and high-quality data from a large dataset has proven challenging. Fluctuating prices and missing data points affect the model's accuracy and the quality of recommendations.

OpenAI Model Fine-Tuning: Fine-tuning OpenAI’s model to provide the most relevant recommendations is a key challenge. Experimenting with prompt variations and parameters is time-consuming, but it is essential for ensuring high-quality responses.

Scalability of Web Crawler: The crawler’s current version works for a limited number of requests. Scaling it up to handle higher volumes while respecting website policies and handling data efficiently will require careful optimization.

Next Steps

This project has made significant progress in its initial stages, with foundational components like the web crawler and data processing pipeline in place. The next steps focus on refining these systems, especially around dynamic content handling and data consistency. Fine-tuning OpenAI’s recommendation generation and completing the user interface will bring us closer to a fully functional recommendation engine.

We are optimistic about overcoming the identified challenges, particularly through enhanced automation in the web crawler, rigorous data handling strategies, and continued iteration on OpenAI model prompts. Upon successful completion, the Best Price Flight Recommender will serve as a valuable tool for users looking for cost-effective, tailored flight options, enhancing the travel planning experience through data-driven insights and recommendations.
