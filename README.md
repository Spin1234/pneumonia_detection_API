# pneumonia_detection_API

You can document your **Pneumonia Detection API** on GitHub using Markdown. Here’s an example `README.md` file with Fetch API code in JavaScript and React.  

---

## **Pneumonia Detection API Documentation**  

### **Base URL**  
```
https://pneumonia-detection-web-app.onrender.com
```

### **1. Predict Pneumonia**  
**Endpoint:**  
```
POST /predict
```

**Request Headers:**  
```json
{
  "Content-Type": "multipart/form-data"
}
```

**Request Body (FormData):**  
- **image** (file) – The chest X-ray image to be analyzed.  

#### **Example: Fetch API in JavaScript**  
```js
const formData = new FormData();
const fileInput = document.querySelector("#fileInput");
formData.append("image", fileInput.files[0]);

fetch("https://pneumonia-detection-web-app.onrender.com/predict", {
  method: "POST",
  body: formData
})
  .then(response => response.json())
  .then(data => console.log("Prediction:", data))
  .catch(error => console.error("Error:", error));
```

---

### **Example: React Implementation**
```jsx
import { useState } from "react";

function PneumoniaDetection() {
  const [file, setFile] = useState(null);
  const [result, setResult] = useState(null);

  const handleFileChange = (event) => {
    setFile(event.target.files[0]);
  };

  const handleSubmit = async (event) => {
    event.preventDefault();
    if (!file) return alert("Please upload an image.");

    const formData = new FormData();
    formData.append("image", file);

    try {
      const response = await fetch(
        "https://pneumonia-detection-web-app.onrender.com/predict",
        { method: "POST", body: formData }
      );
      const data = await response.json();
      setResult(data);
    } catch (error) {
      console.error("Error:", error);
    }
  };

  return (
    <div>
      <h2>Pneumonia Detection</h2>
      <form onSubmit={handleSubmit}>
        <input type="file" onChange={handleFileChange} accept="image/*" />
        <button type="submit">Predict</button>
      </form>
      {result && <p>Prediction: {JSON.stringify(result)}</p>}
    </div>
  );
}

export default PneumoniaDetection;
```

---

### **Response Format**  
```json
{
  "prediction": "Pneumonia",
  "confidence": 0.95
}
```

You can add authentication (if needed), more details about response handling, and error cases. Let me know if you need further refinements! 🚀
