AI Investigator

Overview

AI Investigator is a Python-based digital investigation prototype that combines rule-based evidence analysis with generative AI reasoning.

The project processes a collection of timestamped investigation events, identifies potentially suspicious activity using predefined rules, builds a chronological view of relevant events, detects possible contradictions, and sends the structured evidence to a Groq-hosted language model for deeper analysis.

The notebook is designed to demonstrate how traditional programmatic analysis and generative AI can work together in an investigation workflow.

Features

Stores investigation evidence as timestamped events

Converts raw evidence into structured Python dictionaries

Filters events using predefined suspicious keywords

Builds a suspicious-event timeline

Detects possible relationships between consecutive events

Checks statements against previously identified activity

Assigns rule-based scores and priorities to events

Generates a consolidated investigation report

Uses the Groq Python SDK for AI-powered evidence analysis

Passes both raw evidence and rule-based findings to the AI model

Instructs the AI to distinguish evidence from inference and avoid unsupported facts

Investigation Workflow

Raw Evidence
     |
     v
Evidence Parsing
     |
     v
Structured Events
     |
     +----------------------+
     |                      |
     v                      v
Rule-Based Analysis      Timeline Analysis
     |                      |
     +----------+-----------+
                |
                v
        Investigation Findings
                |
                v
          Groq AI Analysis
                |
                v
        Investigation Report

Technologies Used

Python

Google Colab

Groq Python SDK

Groq Chat Completions API

openai/gpt-oss-20b

Project Structure

AI_Investigator_AI.ipynb
README.md

Evidence Processing

The notebook begins with raw evidence containing timestamps and event descriptions. The evidence is converted into structured records using the following format:

{
    "time": "02:18 AM",
    "message": "Financial database was accessed."
}

These structured records are stored in events_data and are used throughout the investigation pipeline.

Rule-Based Analysis

The rule-based layer searches event messages for predefined indicators such as:

Database access

Data downloads

Unfamiliar login activity

Matching events are collected into suspicious_events and organized into a timeline.

The notebook also compares events to identify sequences and checks statements against other evidence.

Each event can receive a numerical score and a corresponding priority level.

AI Analysis

The AI layer uses the Groq Python SDK and Chat Completions API.

The notebook constructs an evidence text from events_data and combines it with the rule-based findings. This information is supplied to the language model through a structured prompt.

The AI is instructed to analyze:

Suspicious events

Chronological sequences

Possible contradictions

Relationships between events

Evidence requiring further investigation

An overall assessment

The prompt also instructs the model not to create unsupported people, events, motives, timestamps, or facts.

API Key Configuration

The notebook is designed for Google Colab and retrieves the Groq API key from Colab Secrets.

Create a Colab Secret named:

GROQ

The notebook accesses it with:

from google.colab import userdata
from groq import Groq

client = Groq(api_key=userdata.get("GROQ"))

Do not place the API key directly inside the notebook source code.

Installation

Install the Groq package before running the AI section:

!pip install -q groq

Running the Project

Open AI_Investigator_AI.ipynb in Google Colab.

Add the GROQ API key to Colab Secrets.

Run the notebook cells from top to bottom.

Allow the evidence to be parsed into events_data.

Run the rule-based investigation cells.

Run the Groq connection cell.

Run the AI analysis cell.

Review the generated investigation analysis.

Review the consolidated investigation_report.

Investigation Output

The final report contains three primary components:

{
    "evidence": events_data,
    "rule_based_findings": [...],
    "ai_analysis": ai_investigation
}

This provides a single structure containing the original evidence, programmatic findings, and AI-generated analysis.

Important Considerations

The AI component analyzes only the evidence supplied to it. Its output should be treated as an analytical aid rather than definitive proof.

The rule-based and AI layers have different responsibilities. The rule-based layer provides deterministic processing based on predefined conditions, while the AI layer provides natural-language analysis of the available evidence.
