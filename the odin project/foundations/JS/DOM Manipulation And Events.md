# DOM Manipulation And Events - לא גמור
Origin: https://www.theodinproject.com/lessons/foundations-dom-manipulation-and-events

DOM - ראשי תיבות של Document Object Model 
כלומר מודל אובייקט מסמך (מודל של האובייקט שמייצג את המסמך)
במודל זה המסמך מוצג כאובייקט שהמידע שבו בנוי בצורת עץ של צמתים (nodes) עם קשרים בניהם
למשל: 
``` html
<div id="container">
  <div class="display"></div>
  <div class="controls"></div>
</div>
```
ניתן לייצג בצורה:

* container צומת ראש העץ
  * display צומת בן
  * controls צומת בן

למען הדיוק "ראש העץ" בתרשים זה מכוון באופן מקומי, באופן טבעי ראש עץ של מסמך html יהיה תמיד תגית html שבתחילת המסמך. כאשר דף html מומר להיות אובייקט עץ ראש העץ הוא document.

כאשר מסמך html מגיע לדפדפן הוא מתורגם לאובייקט עץ כמו שמתואר למעלה. לכל צומת יש הרבה מאפיינים ולא רק השם. בין המאפיינים יש גם שיטות (פונקציות) שניתן להפעיל על אותו צומת. באמצעות גישה למאפיינים ושיטות אלו ניתו=ן לבצע מניפולציות על האובייקט ובכך לשנות אותו בהתאם לאירועים שקוראים בדף. 

## הוספת אלמנט

* ```element.querySelector(selector)```  מחזיר הפנייה ישירה להתאמה הראשונה של הבורר  
* ```element.querySelectorAll(selectors)```  מחזיר רשימת הצמתים העונים להגדרת הבורר 
  רשימה זו אינה מערך למרות שזה נראה כמו מערך ובאופנים מסויימים מתנהג כמו מערך אבל רשימה זו היא מסוג nodelist ואם רוצים להשתמש בה כמערך (לצורך שימוש בפונקציות מוכרות ממערכים) צריך להפעיל עליה את הפונקציה ```Array.from()``` או להשתמש באופרטור ההפרדה (spread operator).

ניתן ליצור אלמנט חדש שיתווסף לעץ כצומת חדש. באמצעות 
``` javascript
 let div = document.createElement('div');
 ```
 פעולה זו עדיין לא מוסיפה את האלמנט לDOM אלא רק יוצרת אותו בזיכרון כדי להוסיף לDOM ניתן להשתמש בפונקציות הבאות:

 * ```parentNode.appendChild(childNode)``` מוסיף את childNode כצומת בן אחרונה של  parentNode
 * ```parentNode.insertBefore(newNode, referenceNode)``` מוסיף את  newNode לצומת האב parentNode לפני צומת הבן referenceNode

כמו כן ניתן להשתמש ב:
 * ```parentNode.removeChild(child)``` מסיר את צומת הבן מ parentNode ומחזיר הפנייה לבן (שניתן להשתמש בה אם רוצים למשל לשים את הבן במקום אחר במסמך)

## עריכת תוכן של אלמנט  

  ראינו דוגמאות לשימוש בפונקציות אבל כאמור ניתן גם לשנות ערכים של מאפיינים של הצומת. כמו בדוגמה הבא:
```javascript
const div = document.createElement('div'); // יוצר div חדש 
div.style.color = 'blue'; //מגדיר צבע טקסט                     
div.style.cssText = 'color: blue; background: white;'; // מגדיר מספר כללי css
div.setAttribute('style', 'color: blue; background: white;');//מגדיר מאפיין 
  ```

בcss מאפיינים בעלי יותר ממילה אחת מופרדים בשיטת
kebab-cased לעומת JS שמשתמשת בשיטת camelCase ולכן כאשר מוסיפים בקוד JS מאפיינים של CSS אז צריך להמיר גם את הצורה ניתן להבחין בהבדלים להלן:
```javascript
div.style.backgroundColor = "white";
div.style['background-color'] = "white";
div.style.cssText = "background-color: white;";
```
שימו לב לצורות השונות של backgroundColor בקוד למעלה

~~div.style.background-color~~ הפורמט הזה אינו תקין.

### עריכת מאפיינים קיימים

מלבד הוספת מאפיינים ניתן כמובן גם לערוך מאפיינים קיימים:

```javascript
div.setAttribute('id', 'theDiv');
// פעולה זו תדרוס מאפיין שכבר היה קיים
// כי זהו מאפיין ייחודי ואסור שיהיו שניים

div.getAttribute('id');// מחזיר את הערך הנוכחי, אם קיים.

div.removeAttribute('id');// מוחק את המאפיין הנוכחי אם קיים.                                     
```
### עריכת מחלקות CSS
ניתן גם לשנות את המחלקות הCSS המופעלות על האלמנט באופן הבא:

```javascript
div.classList.add('new');                                      
// מוסיף מחלקה חדשה

div.classList.remove('new');                                   
// מסיר מחלקה

div.classList.toggle('active');                                
// מוסיף מחלקה אם אינה קיימת
// אם המחלקה קיימת אז מסיר אותה
```

#### הוספת תוכן
```javascript
div.textContent = 'Hello World!' 
```
ניתן גם להוסיף תוכן שכולל תגיות HTML:

```javascript 
div.innerHTML = '<span>Hello World!</span>';  
```
### השפעת מיקום הקוד
יש לשים לב שלא משנים אלמנט כלשהו במסמך לפני שהוא נוצר. אם קוראים לקובץ הקוד בתחילת המסמך בתוך אלמנט head אזיי האלמנטים שנמצאים בתוך הbody לא נוצרו עדיין ולכן הקוד לא יכול לבצע עליהם מניפולציות. כדי להצליח לבצע מניפולציות על התוכן יש לצרף את הסקריפט בסוף או לפחות אחרי האלמנט אותו אנחנו רוצים לשנות בקוד. 

לחילופין ניתן לציין בתוך התגית בhead שאנחנו רוצים שהקובץ ייטען לאחר טעינת שאר המסמך באופן הבא
```html
<head>
  <script src="js-file.js" defer></script>
</head>
```
יש לשים לב לתוספת defer בתוך התגית.

---
יש להפריד לקובץ נפרד
---
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
###  קבלת פרמטרים לפונקציית אירוע
ניתן לקבל מידע נוסף על האירוע באמצעות הגדרת פרמטרים שהפונקציה מקבלת 

