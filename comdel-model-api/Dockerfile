FROM python:3.12-slim

# Set the working directory inside the container
WORKDIR /app

# Copy the requirements file first (for better layer caching)
COPY requirements.txt .

# Install the dependencies
RUN pip install --no-cache-dir --upgrade pip \
    && pip install --no-cache-dir -r requirements.txt

# Pre-download Hugging Face model & tokenizer so it's cached in the image
RUN python -c "from transformers import AutoTokenizer, AutoModelForSequenceClassification; \
    AutoTokenizer.from_pretrained('KeyzarRasya/yt-com'); \
    AutoModelForSequenceClassification.from_pretrained('KeyzarRasya/yt-com')"

# Now copy the rest of the application code
COPY . .

# Expose the port your FastAPI app will run on
EXPOSE 8000

# Run the FastAPI app using uvicorn
CMD ["uvicorn", "main:app", "--host", "0.0.0.0", "--port", "8000"]
