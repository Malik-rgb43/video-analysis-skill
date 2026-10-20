# video-analysis-skill

סקיל ל-Claude Code שנותן ל-Claude "עיניים" לסרטון: פירוק לפריימים, מדידה, חיתוכים, תמלול (עברית היטב) וניתוח סאונד. הכול רץ על המחשב שלכם.

A Claude Code skill that lets Claude analyse a video: every frame measured, keyframe contact sheets, cut points, a transcript (Hebrew deepest) and a sound analysis. Everything runs locally.

## מה מקבלים

- מדידה של כל פריים וחיתוכים, וכמה זמן נמשך כל שוט.
- גיליונות פריימים עם חותמות זמן ש-Claude מסתכל עליהם כתמונות.
- תמלול של הדיבור (אופציונלי, על המחשב).
- ניתוח סאונד: עוצמה, שקטים, קצב (BPM), טונליות וקצבי ביט.
- דוח שנפתח ב"כיסוי": מה נבדק ומה לא.

## התקנה

דרישות: Python 3.9 ומעלה, [FFmpeg](https://ffmpeg.org/) במערכת.

פותחים את קובץ ה-ZIP לתיקייה (או משבטים את הריפו: `git clone https://github.com/Malik-rgb43/video-analysis-skill`), ואז:

```bash
cd video-analysis-skill
pip install numpy Pillow
python tools/analyze.py --check
```

ואז פותחים את Claude Code **בתוך התיקייה הזאת** (הסקיל נמצא ב-`.claude/skills/video-analysis` ונטען לבד) ואומרים:

> תנתח לי את הסרטון הזה: C:\path\to\video.mp4

אפשר גם לתת ל-Claude Code את התיקייה ולומר: "תתקין את הסקיל הזה".

### תמלול (לא חובה)

```bash
pip install faster-whisper
python tools/transcribe.py --check
```

מודל הדיבור הוא הורדה נפרדת. הכלי לא מוריד אותו בלי הסכמה, ומציג קודם מה יורד. מודל העברית (ivrit-ai) שוקל כ-1.6GB. בלי תמלול מריצים עם `--asr never`.

## שימוש ישיר, בלי Claude

```bash
python tools/analyze.py video.mp4 --out analysis/my-video --detail standard --asr never
```

התוצאה: `measurements.json`, `frames.csv`, `sheets/`, `audio.json`, `transcript.json` ו-`report.md`. הקובץ של הסרטון נקרא בלבד ולא משתנה.

## מגבלות

- מספר החיתוכים שמוצא הכלי אוטומטית הוא הערכה. הוא נבדק על הגיליונות לפני שמצטטים אותו.
- ניתוח הסאונד מבוסס על האות בלבד: הוא לא אומר איזה סאונד זה ולא מזהה שירים. קצב וטונליות הם הערכות.
- סרטון ארוך צורך זיכרון (בערך 5KB לכל פריים). סרטון של שעה ב-60 פריימים לשנייה צריך יותר מ-1GB. מומלץ לחתוך את החלק שרוצים ללמוד.
- התמלול טועה לפעמים בשמות ובמספרים. בודקים אותם.

## מקור

הסקיל והכלים הם חלק מ-[editing-workflow](https://github.com/Malik-rgb43/editing-workflow), ערכת עריכת וידאו עם Claude. כאן יש רק מה שצריך כדי לנתח סרטון. סקילים נוספים שמוזכרים בקובץ SKILL.md (למשל `pro-video-editor`) שייכים לערכה המלאה, והם לא חובה.

## English

Requirements: Python 3.9+, FFmpeg, `numpy`, `Pillow` (and `faster-whisper` for a transcript). Clone the repo, run `python tools/analyze.py --check`, open Claude Code inside the folder and ask it to analyse a video. Automatic cut counts and the tempo/key estimate are estimates to be checked on the sheets; nothing leaves your computer.

License: Apache-2.0.
