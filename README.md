import shutil
from pathlib import Path

TARGET = Path.home() / "Downloads"

CATEGORIES = {
    "Изображения": [".jpg", ".jpeg", ".png", ".gif", ".webp"],
    "Документы": [".pdf", ".docx", ".doc", ".txt", ".xlsx"],
    "Видео": [".mp4", ".mkv", ".avi", ".mov"],
    "Аудио": [".mp3", ".wav", ".ogg"],
    "Архивы": [".zip", ".rar", ".7z"],
}

for f in TARGET.iterdir():
    if f.is_file() and f.name != "organizer.py":
        folder = next((k for k, v in CATEGORIES.items() if f.suffix.lower() in v), "Другое")
        (TARGET / folder).mkdir(exist_ok=True)
        shutil.move(str(f), str(TARGET / folder / f.name))
        
