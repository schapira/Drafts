# ES6
המונח ECMAScript, או ES, היא גרסה סטנדרטית של JavaScript.
 מכיוון שכל הדפדפנים הגדולים פועלים לפי
 מפרט זה,
 ניתן להשתמש במונחים ECMAScript ו-JavaScript 
 לסירוגין, והכוונה לאותה משמעות.

גרסת JavaScript הקודמת נקראה
ES5 (ECMAScript 5),
גרסה זו הסתיימה ב 2009
  למרות שניתן עדיין יכול לכתוב תוכניות ב-ES5, 
  שפת JavaScript מתפתחת כל הזמן, ותכונות חדשות משוחררות מדי שנה.

לעומת זאת ES6, שיצא ב-2015, הוסיף תכונות חדשות רבות ועוצמתיות לשפה. 

## מרחבי ההשפעה של var לעומת let

כאשר מגדירים משתנה באמצעות var
 הוא מוגדר באופן גלובלי למעט אם הוא מוגדר בתוך פונקציה ואז הוא מקומי לאותה פונקציה
  בשימוש ב let ההתנהגות דומה למעט מספר הבדלים משמעותיים
  כאשר פוקנציה מחזירה משתנה שהוגדר באמצעות var היא מחזירה קישור לתא, ואם נעשה עדכון של אותו תא אזיי לא תהיה שמירה של הערך המקורי.
  
  לעומת זאת בשימוש בlet כאשר המשתנה מוחזר בפונקציה, אין החזרה של קישור לתא, כי הוא כבר לא קיים אלא מוחזר הערך שהיה באותו זמן נתון.

## שינוי מערך שהוגדר באמצעות const

אובייקטים, כולל מערכים ופונקציות שמוגדרים באמצעות const עדיין ניתנים לשינוי
כלומר, הערכים הפנימיים שלהם אינם נעולים. ההגדרה שלהם באמצעות const רק מונעת לשנות את הגדרת האב ולא את הגדרת הבנים/מאפיינים/צאצאים

### מניעת עדכון אובייקטים

כאמור שימוש בconst אינו מונע עדכון הערכים הפנימיים של מערך או אובייקט. כדי למנוע שינוי ערכים פנימיים ניתן להשתמש ב
Object.freeze.

```javascript 
Object.freeze(obj);
```

## כתיבת פונקציות אנונימיות
```javascript
const myFunc = function() { }
```
ניתן גם להגדיר ככה: 

```javascript
const myFunc = () => { }
```
וכאשר אין יותר מדיי תוכן לפוקנציה עצמה ניתן אפילו לקצר עוד יותר:
```javascript
 const myFunc = () => "value";
```
### פונקציות אנונימיות עם פרמטרים
כדי לכתוב פונקציה אנונימית עם פרמטרים
ניתן להשתמש במבנה הבא:
```javascript
const doubler = (item) => item * 2;
```
המשמעות בדוגמה זה פונקציה בשם doubler שמקבלת item כפרמטר ומחזירה אותו כפול 2.
## הגדרת ערכי ברירת מחדל לפרמטרים בפוקנציות
ניתן לקבוע ערכים אוטומטיים כברירת מחדל בפונקציות באופן הבא: 
```javascript
const greeting = (name = "Anonymous") => "Hello " + name;
```
בדוגמה הזו לפרמטר name יש ערך ברירת מחדל 
"Anonymous"
### "עוד..." כפרמטר
שימוש בניסוח הזה
```javascript
function howMany(...args) { }
```
מאפשר לקבל מספר בלתי מוגדר ובלתי מוגבל של פרמטרים בתור מערך.

### בין "עוד..." למערך
ספריית [Math](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Math) 
נמצאת בין הספריות שמקבלים כברירת מחדל יש בה הרבה קבועים שנדרשים לביצוע פעולות מתימטיות (π, e ועוד) 
כמו כן פעולות מתימטיות שמרחיבות את הפעולות הבסיסיות של השפה כמו sin, cos וכו'

הפעולה max מוגדרת להחזיר את הערך המקסימלי מתוך רשימת הערכים שהתקבלו אליה.

```javascript console
Math.max(3,6,2,9,1);
> 9
```
הערכים שהפונקציה מקבלת הם כמו ...args 
לכאורה מדובר במערך, אבל זהו לא בדיוק מערך שכן:
```javascript console
let arr=[3,6,2,9,1];
Math.max(arr);
> NaN
```
הפונקציה לא יכולה לקבל מערך אלא רשימת ערכים. בשביל שהיא תוכל לפעול על מערך צריך 'להמיר' אותו לצורת רשימת ערכים באופן הבא: 
```javascript console
let arr=[3,6,2,9,1];
Math.max(...arr);
> 9
```
השלוש נקודות בהתחלה הופכות את המערך לרשימת ערכים, זה נקרא פעולת פריסה (spread operator)

## Destructuring Assignment
### Extract Values from Objects
Destructuring assignment is special syntax introduced in ES6, for neatly assigning values taken directly from an object.

Consider the following ES5 code:

### TODO


* [ ] Use Destructuring Assignment to Extract Values from Objects
* [ ] Use Destructuring Assignment to Assign Variables from Objects
* [ ] Use Destructuring Assignment to Assign Variables from Nested Objects
* [ ] Use Destructuring Assignment to Assign Variables from Arrays
* [ ] Use Destructuring Assignment with the Rest Parameter to Reassign Array Elements
* [ ] Use Destructuring Assignment to Pass an Object as a Function's Parameters
* [ ] Create Strings using Template Literals
* [ ] Write Concise Object Literal Declarations Using Object Property Shorthand
* [ ] Write Concise Declarative Functions with ES6
* [ ] Use class Syntax to Define a Constructor Function
* [ ] Use getters and setters to Control Access to an Object
* [ ] Create a Module Script
* [ ] Use export to Share a Code Block
* [ ] Reuse JavaScript Code Using import
* [ ] Use * to Import Everything from a File
* [ ] Create an Export Fallback with export default
* [ ] Import a Default Export
* [ ] Create a JavaScript Promise
* [ ] Complete a Promise with resolve and reject
* [ ] Handle a Fulfilled Promise with then
* [ ] Handle a Rejected Promise with catch
