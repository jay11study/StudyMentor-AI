# Part 4 – LLM Powered Feature: Model Prediction Explanation Pipeline

# Table of Contents

1. Project Overview
2. Selected Track
3. LLM API Integration
4. Prompt Design
5. Temperature Comparison
6. Structured Output Validation
7. PII Guardrail
8. End-to-End Prediction Explanation Pipeline
9. Validation Results
10. Challenges Faced and Solutions
11. Conclusion

# Project Overview

This notebook demonstrates an LLM-powered feature built on top of the machine learning model developed in Part 3.

The best machine learning model saved as `best_model.pkl` is loaded and used to predict whether a student will pass or fail. The predicted class and prediction probability are then sent to a Large Language Model (LLM), which generates a structured explanation in JSON format.

The notebook also demonstrates prompt engineering, structured JSON validation, temperature comparison and safety guardrails.

# Selected Track

Track C – Model Prediction Explanation Pipeline

Three manually created student records were passed through the trained machine learning model.

For each student:

- Features were encoded.
- The trained model predicted the class.
- Prediction probability was calculated.
- The prediction information was sent to the LLM.
- The LLM returned a structured JSON explanation.
- The response was validated against a predefined JSON schema.

# LLM API Integration

The notebook uses the OpenRouter API through the Python `requests` library.

The API key is stored securely in an environment variable instead of being hardcoded inside the notebook.

A reusable `call_llm()` function was created to:

- send prompts to the LLM
- receive responses
- handle API errors
- return the generated content

A simple test prompt was executed before building the complete pipeline to verify that the API connection worked successfully.

# Prompt Design

A system prompt was created to instruct the LLM to behave as an educational AI assistant.

The prompt instructs the model to:

- explain the machine learning prediction
- return only valid JSON
- avoid Markdown
- avoid code blocks
- avoid additional explanations
- include exactly five required fields

The user prompt contains:

- student feature values
- predicted class
- prediction probability

The LLM returns a JSON explanation containing:

- prediction_label
- confidence_level
- top_reason
- second_reason
- next_step

Temperature was set to 0 because structured JSON generation requires deterministic and consistent outputs.

# Temperature Comparison

The LLM was tested using two temperature values.

- Temperature = 0
- Temperature = 0.7

Both responses successfully generated prediction explanations.

Temperature 0 produced more consistent and predictable responses.

Temperature 0.7 produced slightly different wording while preserving the same overall meaning.

For structured JSON generation, temperature 0 is preferred because it reduces randomness and improves reproducibility.

# Structured Output Validation

A JSON schema was created using the `jsonschema` library.

The schema validates five required fields:

- prediction_label
- confidence_level
- top_reason
- second_reason
- next_step

Each LLM response is processed using the following steps:

- remove unnecessary whitespace
- extract the JSON object
- parse using `json.loads()`
- validate using `jsonschema.validate()`

If validation fails, a fallback dictionary containing `None` values is returned.

This prevents the notebook from stopping because of malformed LLM responses.

# PII Guardrail

A regular expression guardrail was implemented before every LLM call.

The guardrail checks for:

- email addresses
- phone numbers

If personally identifiable information (PII) is detected, the LLM request is blocked.

The notebook demonstrates both cases:

- input containing an email address (blocked)
- input without PII (allowed)

This prevents sensitive personal information from being sent to the external LLM service.

# End-to-End Prediction Explanation Pipeline

The complete pipeline performs the following steps:

1. Load the trained machine learning model.
2. Encode manually created student records.
3. Predict pass or fail using the model.
4. Calculate prediction probability.
5. Send prediction information to the LLM.
6. Receive a structured JSON explanation.
7. Validate the JSON response.
8. Display prediction results and validation status.

Three different student records were successfully processed through the pipeline.

# Validation Results

Each student record produced:

- predicted class
- prediction probability
- LLM explanation
- validation status

Most responses successfully passed JSON schema validation.

Whenever invalid JSON or unexpected responses were returned, the validation function safely handled the error and returned a fallback response without interrupting the pipeline.

# Challenges Faced and Solutions

## Feature Encoding

Initially, manually created student records could not be used directly because the trained model expected one-hot encoded features.
An `encode_record()` function was created to generate the same feature structure used during model training.

## API Key Loading

The notebook initially could not detect the API key.
The `python-dotenv` package was used to load the `.env` file, allowing the API key to be accessed securely through an environment variable.

## OpenRouter Model Availability

The originally selected free model returned a 404 error because the endpoint was no longer available.
The model was changed to `openrouter/free`, allowing OpenRouter to automatically select an available free model.

## JSON Validation

Some LLM responses did not exactly match the required schema.
The validation function was updated to detect parsing errors and schema validation errors while returning a fallback response instead of stopping execution.

## Unexpected API Responses

Some responses included additional text such as:

User Safety: safe
before the JSON object.

The validation function was modified to extract only the JSON portion before parsing.
This allowed valid responses to be processed successfully.

## Prompt Refinement

Early prompts sometimes produced additional explanations instead of pure JSON.

The system prompt was refined to explicitly instruct the model to:

- return only JSON
- avoid Markdown
- avoid extra explanations
- avoid safety labels
- include only the required fields

This improved response consistency.

# Conclusion

The LLM-powered prediction explanation pipeline was successfully implemented.

The notebook demonstrates:

- secure API integration
- prompt engineering
- structured JSON generation
- schema validation
- PII protection
- prediction explanation using the trained machine learning model

This completes the final stage of the StudyMentor AI project by combining traditional machine learning with Large Language Models to provide understandable prediction explanations while maintaining structured output validation and basic safety controls.