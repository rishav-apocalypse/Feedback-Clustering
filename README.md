# Feedback-Clustering
A feedback analysis pipeline that fetches student reviews from Google Sheets, clusters them using semantic embeddings and KMeans, and summarizes each cluster with auto-generated labels using Google Gemini.

#  Student Feedback Clustering and Summarization Pipeline

This project builds a full NLP pipeline that takes student feedback from a **Google Sheet**, clusters similar responses using **KMeans**, and summarizes each group using **Google Gemini**. It also dynamically stores and retrieves data using **LanceDB** for future query-based insights.

---

##  Pip Installs

-pip install langchain lancedb langchain_community requests langchainhub
-pip install langchain google-generativeai
-pip install faiss-cpu lancedb tiktoken
-pip install scikit-learn
-pip install python-docx

---

## App Script Code
function doGet() {  
  var sheet = SpreadsheetApp.getActiveSpreadsheet().getSheetByName("Form Responses 1"); // change name as needed  
  if (!sheet) {  
    return ContentService.createTextOutput("Sheet not found").setMimeType(ContentService.MimeType.TEXT);  
  }  
   
  var data = sheet.getDataRange().getValues();  
  var headers = data.shift();  
  var output = data.map(row => {  
    var obj = {};  
    row.forEach((cell, i) => obj[headers[i]] = cell);  
    return obj;  
  });   
  
  return ContentService.createTextOutput(JSON.stringify(output))  
    .setMimeType(ContentService.MimeType.JSON);  
}  
  
---

##  Features

- Fetch live feedback from **Google Sheets**
- Embed and cluster feedback using **HuggingFace embeddings** + **KMeans**
- Store vectors dynamically in **LanceDB**
- Summarize and auto-label each cluster using **Gemini LLM**
- Export summaries into a `.docx` report

---

