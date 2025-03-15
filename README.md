# pneumonia_detection_API_documentation

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

### **Example: React Implementation Alternative**
```jsx
import React, { useState } from "react";


const Home = () => {

    const [url, uurl] = useState('');
    const [image, setImage] = useState(null);
    const [predict, setPredict] = useState('');

    const handleImage = (e) => {
        if (e.target.files[0]) {
            document.getElementById('btn').style.display = 'none';
            setPredict('');
            uurl(URL.createObjectURL(e.target.files[0]));
            setImage(e.target.files[0]);
            document.getElementById('btn').style.display = 'block';
        }
        else {
            uurl("");
            setImage("");
            setPredict("");
            document.getElementById('btn').style.display = 'none';
        }
    }

    const handleClick = async () => {
        if (!image) {
            alert("Please select an chest x-ray image to predict....")
        }
        else {
            const formData = new FormData();
            formData.append('file', image);
            const response = await fetch("https://pneumonia-detection-web-app.onrender.com/predict", {
                method: 'POST',
                body: formData
            });
            const data = await response.json();
            console.log(data);
            setPredict(data.Prediction);
        }
    }


    return (
        <div className="container mt-5">
  <div className="text-center">
    <h2 className="mb-4">Pneumonia Detection</h2>
  </div>
  <div className="row justify-content-center align-items-start">
    {/* Image and Input Section */}
    <div className="col-md-6 text-center">
    <p>Upload chest x-ray image</p>
      <input
        type="file"
        accept="image/*"
        onChange={handleImage}
        className="form-control mb-3"
        style={{ maxWidth: "400px", margin: "0 auto" }}
      />
      <img
        src={url}
        alt="image comes here...."
        className="img-fluid mb-3"
        style={{ maxHeight: "350px", maxWidth: "100%", borderRadius: "10px" }}
      />
        <button
          className="btn btn-primary"
          id="btn"
          style={{ 'display': 'none' }}
          onClick={handleClick}
        >
          Predict
        </button>
    </div>

    {/* Prediction Result Section */}
    <div className="col-md-6">
      {predict ? (
        <div className="card text-center">
          <div className="card-header bg-primary text-white">
            <h5 className="mb-0">Prediction Result</h5>
          </div>
          <div className="card-body">
            <p className="card-text" style={{ fontSize: "1.2rem" }}>
              <strong>{predict}</strong>
            </p>
          </div>
        </div>
      ) : (
        <div className="text-center text-muted">
          <p>Prediction result will appear here.</p>
        </div>
      )}
    </div>
  </div>
</div>

    )
}

export default Home;
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
