In an `<input>` field in HTML (used in PHP as well), the `type` attribute specifies what kind of input the field accepts. Here are the **most common** values for the `type` attribute:  

---

### **🔹 Common `type` Attributes for `<input>`**
| Type | Description |
|------|------------|
| `text` | Single-line text input (default). |
| `password` | Hides input characters (e.g., for passwords). |
| `email` | Requires a valid email format. |
| `number` | Allows only numerical input. |
| `tel` | For phone numbers (no validation). |
| `url` | Requires a valid URL format. |

---

### **🔹 Numeric & Range Inputs**
| Type | Description |
|------|------------|
| `number` | Allows only numbers, can have min/max values. |
| `range` | Creates a slider to select a numeric value. |

```html
<input type="number" min="1" max="10">
<input type="range" min="0" max="100" step="5">
```

---

### **🔹 Date & Time Inputs**
| Type | Description |
|------|------------|
| `date` | Select a date (YYYY-MM-DD). |
| `time` | Select a time (HH:MM). |
| `datetime-local` | Select date and time (YYYY-MM-DDTHH:MM). |
| `month` | Select a month (YYYY-MM). |
| `week` | Select a week (YYYY-W##). |

```html
<input type="date">
<input type="time">
<input type="datetime-local">
```

---

### **🔹 File & Media Inputs**
| Type | Description |
|------|------------|
| `file` | Allows file uploads. |
| `image` | Submit an image as a button. |

```html
<input type="file">
<input type="image" src="submit.png">
```

---

### **🔹 Selection Inputs**
| Type | Description |
|------|------------|
| `radio` | Select one option from multiple. |
| `checkbox` | Select multiple options. |

```html
<input type="radio" name="gender" value="male"> Male
<input type="radio" name="gender" value="female"> Female

<input type="checkbox" name="subscribe" value="yes"> Subscribe to Newsletter
```

---

### **🔹 Special Inputs**
| Type | Description |
|------|------------|
| `hidden` | Stores hidden values. |
| `submit` | Button to submit a form. |
| `reset` | Button to reset a form. |
| `button` | Custom button (requires JavaScript). |
| `search` | Search field (styled differently in some browsers). |
| `color` | Opens a color picker. |

```html
<input type="hidden" name="user_id" value="123">
<input type="color">
<input type="submit" value="Send">
<input type="reset">
```

---

### **🔹 Example: Full Form with Different Input Types**
```html
<form>
    <label for="name">Name:</label>
    <input type="text" id="name">

    <label for="email">Email:</label>
    <input type="email" id="email">

    <label for="age">Age:</label>
    <input type="number" id="age">

    <label for="dob">Date of Birth:</label>
    <input type="date" id="dob">

    <label for="color">Favorite Color:</label>
    <input type="color" id="color">

    <label for="file">Upload File:</label>
    <input type="file" id="file">

    <button type="submit">Submit</button>
</form>
```

Would you like an example in PHP as well? 🚀