# 🍳 JARVIS Kitchen: The Self-Correcting Culinary AI Agent

![Agent Status](https://img.shields.io/badge/Agent-Active-success) ![Gemini](https://img.shields.io/badge/AI-Gemini%201.5%20Flash-blue) ![Type](https://img.shields.io/badge/Architecture-Multi--Agent-orange)

**A multimodal agentic system that sees your ingredients, verifies health goals via a Critic loop, and speaks your meal plan hands-free.**

> **Capstone Project Submission** for the Google AI Agents Intensive (Concierge Agents Track).

---

## 📖 Table of Contents
- [The Problem](#-the-problem)
- [The Solution](#-the-solution)
- [System Architecture](#-system-architecture)
- [Technical Implementation](#-technical-implementation-course-concepts)
- [Live Demo & Outputs](#-live-demo--outputs)
- [How to Run](#-how-to-run)
- [Future Roadmap](#-future-roadmap)

---

## 🧠 The Problem
**Decision Fatigue & Friction.**
Every day, households stare at random ingredients in the fridge, unsure how to combine them.
1.  **Static Apps:** Recipe apps don't know what you *actually* have.
2.  **Health Misalignment:** They rarely verify if a recipe *truly* fits specific goals (e.g., "Muscle Gain") accurately.
3.  **Hands-Busy:** Cooking requires hands; reading text on a phone screen is cumbersome.

## 💡 The Solution
**JARVIS Kitchen** is not a chatbot; it is a closed-loop **Agentic Operating System**.
*   **It Sees:** Uses Computer Vision to identify raw ingredients.
*   **It Verifies:** Uses a "Critic Agent" to mathematically audit the recipe before suggesting it.
*   **It Speaks:** Uses synthesized audio to brief the user hands-free.
*   **It Acts:** Automatically generates and saves a shopping list for missing items.

---

## 🏗 System Architecture

This system utilizes a **Sequential Multi-Agent Chain** with a **Self-Correction Loop**.

<img width="719" height="776" alt="Screenshot (65)" src="https://github.com/user-attachments/assets/633798e1-5bf7-4240-96de-03ae4450d965" />


### The Agent Chain
1.  **👁️ Vision Agent (The Input):**
    *   **Role:** Processes raw image data to identify ingredients.
    *   **Goal:** Grounds the AI in reality, eliminating manual data entry.
2.  **👨‍🍳 Chef Agent (The Reasoning):**
    *   **Role:** Drafts a culinary plan based on the detected ingredients.
    *   **Context:** Checks the persistent `user_profile` for goals (e.g., "High Protein").
3.  **⚖️ Critic Agent (The Guardrail):**
    *   **Role:** **Agent Evaluation.** It reviews the Chef's output.
    *   **Logic:** If the recipe does not meet the macro-nutrient criteria, it *rejects* the plan and forces a retry.
4.  **🗣️ Narrator Agent (The Voice):**
    *   **Role:** Summarizes the final plan and triggers the Audio Tool.
5.  **🛒 Shopper Agent (The Hands):**
    *   **Role:** Identifies missing items and triggers the File Tool.

---

## 🏆 Technical Implementation (Course Concepts)

I demonstrated mastery of 4 key concepts from the AI Agents Intensive:

### 1. Multi-Agent Systems (Sequential + Evaluation)
Instead of a single prompt, I orchestrated specific personas. The **Critic Agent** is the standout feature, implementing **Self-Correction** to ensure the AI doesn't hallucinate healthy meals that are actually unhealthy.

### 2. Tool Use (Function Calling)
The agents are equipped with custom Python tools to affect the real world:
*   `generate_audio_briefing(text)`: Wraps **gTTS** to generate .mp3 files.
*   `save_shopping_list(content)`: Interacts with the local file system to persist data.

### 3. Sessions & Memory
A persistent `user_profile` dictionary acts as **Long-Term Memory**.
*   It stores **Allergies** (e.g., "Peanuts").
*   It stores **Goals** (e.g., "Muscle Gain").
*   This context is injected into every agent step, ensuring safety and personalization.

### 4. Observability & Robustness
*   **Auto-Discovery Protocol:** The code includes a dynamic model selector that tests API endpoints (Flash vs. Pro) to prevent crashes due to version deprecation.
*   **Console Logging:** Each agent step is color-coded in the output for easy debugging.

---

## 🔉 Live Demo & Outputs

When the system runs, it produces two tangible artifacts:

### 1. Audio Briefing (`briefing.mp3`)
The agent speaks to the user:
> *"I've identified eggs and spinach. To support your muscle gain goal, I suggest a Frittata which provides 25g of protein. I have added feta cheese to your shopping list."*

### 2. Shopping List (`shopping_list.txt`)
A physical text file saved to the disk:
```text
[JARVIS SHOPPING LIST]
- Feta Cheese
- Olive Oil
- Black Pepper 

```
### 🚀 How to Run
Option 1: Google Colab (Recommended)
For the best interactive experience (including the Audio Dashboard), run the notebook directly in the browser:

Open Gen_AI_Agent_Capstone_Project.ipynb in Google Colab.
Add your API Key securely when prompted.
Run All Cells.

Option 2: Run Locally
Prerequisites

Python 3.9+
Google Gemini API Key
1. Clone the Repository
```text
git clone https://github.com/Himanshu431-coder/Google-Gen-AI-Coursework.git
cd Google-Gen-AI-Coursework
```
2. Install Dependencies
```text
pip install -r requirements.txt
```
3.Run the Agent
```text
# Set your API Key (Linux/Mac)
export GOOGLE_API_KEY="your_key_here"

# Run the script
python agent_logic.py
```

### 🔮 Future Roadmap
Hardware Integration: Connect the Vision Agent to a live Raspberry Pi camera feed for real-time pantry tracking.
API Action: Upgrade the Shopper Agent to connect directly to the Instacart API for one-click ordering.
Voice Input: Add Whisper integration to allow the user to speak back to the agent.

