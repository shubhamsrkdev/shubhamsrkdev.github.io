---
title: "Movie Recommendation System (LLM-Based)"
excerpt: "A personalized movie recommendation tool powered by Large Language Models (LLMs) like OpenAI's GPT."
collection: portfolio
---

[![GitHub Repository](https://img.shields.io/badge/GitHub-Repository-blue)](https://github.com/shubhamsrkdev/Movie-Recommendation-System-LLM-Based)

Welcome to the **Movie Recommendation System (LLM-Based)**, a personalized movie recommendation tool powered by Large Language Models (LLMs) like OpenAI's GPT. This project dynamically generates movie suggestions based on user preferences without relying on a static, local movie database.

## 🌟 Key Features
- **Dynamic Recommendations:** Leverages LLM capabilities to fetch the latest and most relevant movie recommendations.
- **Interactive Experience:** Asks users five general questions to understand their preferences, including genre, language, mood, release year, and popularity.
- **Modular Design:** Organized into separate modules for scalability and maintainability.
- **No Local Database Required:** Utilizes real-time LLM queries, eliminating the need for maintaining movie data locally.

## 🔧 How It Works
1. **User Interaction:**
   - The system prompts the user with five questions about their movie preferences.
   - These questions cover aspects like preferred genre, language, mood, release year, and popularity level.

2. **LLM Querying:**
   - The collected preferences are formatted into a prompt.
   - The prompt is sent to OpenAI's API, which responds with a curated list of movie recommendations based on the inputs.

3. **Results Display:**
   - The recommended movies are displayed in a user-friendly format.

## 🌐 Repository Link
You can find the complete project on GitHub: [Movie Recommendation System (LLM-Based)](https://github.com/shubhamsrkdev/Movie-Recommendation-System-LLM-Based)

## 💡 Technologies Used
- **Python 3.7+**: Core programming language used for the system.
- **OpenAI API**: Provides the LLM for dynamic movie recommendations.
- **Command-Line Interface**: For seamless user interaction.

## 📖 Project Structure
```
Movie-Recommendation-System-LLM-Based/
├── main.py                # Entry point of the application
├── recommender.py         # Handles recommendation logic with the LLM
├── user_input.py          # Manages user interaction and input collection
├── api_communicator.py    # Communicates with the OpenAI API
├── utils.py               # Contains helper functions
└── requirements.txt       # Lists all dependencies
```

## 🔄 Example Workflow
1. **Run the Program:**
   ```bash
   python main.py
   ```
2. **Answer the Questions:**
   - What genre do you prefer? *Comedy*
   - Which language do you prefer? *English*
   - What mood do you prefer? *Happy*
   - What is the minimum release year you'd like? *2010*
   - On a scale of 1-10, how popular do you want the movie to be? *8*

3. **View Recommendations:**
   Recommended Movies:
   - The Grand Budapest Hotel
   - Crazy Rich Asians
   - The Intern
   - La La Land

---

Explore personalized movie recommendations with the power of LLMs! 🎬

