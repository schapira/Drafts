# שינויים ב DOM בתגובה לאירועים
DOM And Events - לא גמור
Origin: https://www.theodinproject.com/lessons/foundations-dom-manipulation-and-events

## אירועים - Events
שלושה דרכים להצמיד פונקציה לאירוע שקורה באלמנט:
 * inline:
  ```html
  <button onclick="alert('Hello World')">Click Me</button>
  ```
  ניתן להחליף לשם פונקציה שקיימת בקובץ אחר באופן הבא:
  ```html
  <button onclick="alertFunction()">CLICK</button>
  ```
 * by id
  ```javascript
  const btn = document.querySelector('#btn');
   //from the html: <button id="btn">Click Me</button>
  btn.onclick = () => alert("Hello World");
  ```
 * או:
  ```javascript
  btn.addEventListener('click', () => {
  alert("Hello World");
});
  ```
### קבלת פרמטרים לפונקציית אירוע
ניתן לקבל מידע נוסף על האירוע באמצעות הגדרת פרמטרים שהפונקציה מקבלת 
```javascript
btn.addEventListener('click', function (e) {
  console.log(e);
});
```
זוהי פונקצייה חוזרת (callback function) הפרמטר e הוא אובייקט עם מידע על האירוע עצמו
### הוספת מאזין למספר צמתים
אם קיימים מספר צמתים (אובייקטים בדף) שאנחנו מעוניינים לתת להם מאזין (להפעיל עליהם פונקציה מסויימת כאשר אירועי כלשהו קורה)
למשל, אם יש לנו גלריה של תמונות ואנחנו רוצים התנהגות מסויימת שתקרה בלחיצה על כל אחת מהתמונות (למשל: הגדלה של התמונה)

