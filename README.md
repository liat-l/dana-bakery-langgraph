# Dana's Bakery: From a Story to a Graph

תרגיל 2 בקורס סוכני AI: מערכת הזמנות דטרמיניסטית ב־Python ו־LangGraph עם הסברים בעברית, ללא LLM וללא מפתח API.

## הרצה ב־Google Colab

1. פתחו את [Google Colab](https://colab.research.google.com/).
2. בחרו File → Upload notebook והעלו את `dana_bakery_langgraph.ipynb`.
3. בחרו Runtime → Run all בסביבת Python 3 רגילה; אין צורך ב־GPU.

המחברת עצמאית וכוללת התקנה, קוד, תרשים, דוגמת הפעלה ובדיקות. אין צורך להעלות את קובצי ה־Python הנלווים. לא נוצר קישור שיתוף ל־Colab ולא הוגדרו הרשאות שיתוף.

## מבנה הגרף

אימות → מלאי → עד שתי החלפות לפי הצורך → תמחור → משלוח → הודעה → סיום. קלט לא תקין או חוסר מלאי עוברים ישירות להודעה ולסיום עם סכום 0 וללא מוצר שנמכר.

המלאי מתאפס לכל הפעלה. הנחה של 15% חלה רק כשסכום המוצרים גדול מ־150 ₪ ולא ביום שישי. משלוח בירושלים עולה 20 ₪; עיר אחרת או ריקה מובילה לאיסוף חינם. מלאי מספיק נדרש לכל הכמות.

## הרצה מקומית

```sh
python -m pip install -r requirements.txt
python test_bakery.py
```

`bakery.py` הוא עותק של המימוש שבמחברת. `test_bakery.py` מכיל בדיקות עם תוצאות צפויות ובדיקת 924 צירופים. `build_notebook.py` מייצר מחדש את המחברת (דורש nbformat). אין להריצו על מחברת עם פלט שרוצים לשמור.

`draw_mermaid_png()` מצייר דרך Mermaid.ink ונדרש עבורו חיבור לרשת. עיבוד הזמנות אינו דורש רשת. תיעוד: [LangGraph](https://docs.langchain.com/oss/python/langgraph/graph-api), [ציור PNG](https://reference.langchain.com/python/langchain-core/runnables/graph/Graph/draw_mermaid_png).

## תוצאות אימות

ב־8 בנובמבר 2026 הורצה המחברת כולה בגרעין Python חדש בסביבה המקומית. כל 952 הבדיקות עברו (28 מקרים מפורשים ועוד 924 צירופים), נבדקו ששת שדות הפלט בכל מקרה, ותרשים PNG נוצר ונשמר בתוך פלט המחברת. נבדק גם המימוש הנפרד באמצעות `test_bakery.py`. הרצה בשרת Google Colab עצמו טרם נבדקה.

לא בוצע פרסום ל־GitHub: `gh auth status` דיווח שהאסימון של `liat-l` אינו תקף. גם זהות מחבר Git אינה מוגדרת בסביבה, ולכן לא נוצר commit בשם משוער. להשלמת הפרסום, התחברו עם `gh auth login -h github.com`, הגדירו שם ודוא״ל למחבר Git וצרו מאגר בשם `dana-bakery-langgraph`. לחלופין ניתן ליצור את המאגר באתר GitHub ולהעלות אליו את הקבצים. אין להעלות את `.venv`.

להרצה חוזרת של המחברת המקומית עם שמירת הפלטים התקינו גם `nbformat nbclient ipykernel` והריצו `python verify_notebook.py`.
