
# 🤖 AI Content Automation Framework

This project automatically fetches articles from trusted sources (RSS feeds, Substack, blogs), summarizes them using Hugging Face models, categorizes them, and pushes them to a WordPress site for human curation.

---

## 📁 Folder Structure

| Folder/File      | Purpose                                                                 |
|------------------|-------------------------------------------------------------------------|
| `app/api/`       | FastAPI routes (e.g., `/summarize`, `/health`)                         |
| `app/core/`      | App configuration and `.env` loading                                   |
| `app/fetcher/`   | Fetches articles using RSS, BeautifulSoup, or Selenium (for JS pages)  |
| `app/models/`    | Loads Hugging Face summarization and categorization models             |
| `app/pipelines/` | Core pipeline that fetches → summarizes → categorizes → publishes      |
| `app/schemas/`   | Defines data structures using Pydantic (request/response formats)       |
| `app/services/`  | Business logic: summarization, deduplication, WordPress integration     |
| `app/utils/`     | Helper functions (e.g., cleaning, logging)                              |
| `app/main.py`    | Entry point for the FastAPI app                                         |
| `scheduler/`     | Runs the pipeline on a schedule (e.g., every few hours)                 |
| `data/`          | Stores deduplication log or cache of fetched articles                   |
| `.env`           | Stores sensitive environment variables                                  |
| `requirements.txt` | List of required Python packages                                     |

---

## 🚀 Getting Started

Follow these steps to clone and run this project locally.

### 1. Clone the Repository

```bash
git clone https://github.com/dhruvi5319/ai-content-hub.git
cd ai-content-hub
```

### 2. Create and Activate a Virtual Environment

```bash
python -m venv venv
source venv/bin/activate  # Windows: venv\Scripts\activate
```

### 3. Install Dependencies

```bash
pip install -r requirements.txt
```

---

## ⚙️ Setup Environment Variables(For now this folder is pushed on git)

Create a `.env` file in the root folder and add:

```env
WP_USERNAME=your_wp_username
WP_APP_PASSWORD=your_wp_app_password
MODEL_SUMMARIZER=facebook/bart-large-cnn
MODEL_CATEGORIZER=facebook/bart-large-mnli
```

---

## ▶️ Running the App

### 1. Run the FastAPI server (for testing)

```bash
uvicorn app.main:app --reload
```

Visit [http://127.0.0.1:8000/docs](http://127.0.0.1:8000/docs) to access Swagger UI.

---

## ✅ Contributions

Each team member should:
- Use the appropriate folder for their role
- Commit regularly with meaningful messages
- Use `.gitkeep` files to preserve folder structure

---

## 🧠 Notes

- BeautifulSoup is used for fast parsing of static HTML
- Selenium is used only for JavaScript-heavy sites (e.g., Substack)
- Deduplication prevents reposting the same article
- All articles are pushed as **drafts** to WordPress for curator review

---