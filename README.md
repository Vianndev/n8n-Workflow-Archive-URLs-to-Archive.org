# **n8n Workflow: Archive URLs to Archive.org**

This repository contains an n8n workflow automation node to post URLs to [Archive.org](https://archive.org) using the S3-like API. This workflow allows you to automate the archiving of web pages.

![image](https://github.com/user-attachments/assets/3a4492de-d0e7-4d86-b9a9-bf5b702362d8)

## **Prerequisites**

1. **Internet Archive Account**:
   - Create an account at [archive.org](https://archive.org/account/login).
   - If you already have an account, log in.

2. **IA-S3 Credentials**:
   - Go to [https://archive.org/account/s3.php](https://archive.org/account/s3.php).
   - Generate your **Access Key** and **Secret Key**.
   - Keep these credentials secure.

3. **n8n Setup**:
   - Install and set up n8n (https://n8n.io/).

## **Workflow**

The workflow uses the **HTTP Request** node in n8n to send a POST request to archive.org's API.

### **JSON Workflow**
```json
{
  "nodes": [
    {
      "parameters": {
        "method": "POST",
        "url": "https://web.archive.org/save",
        "sendHeaders": true,
        "headerParameters": {
          "parameters": [
            {
              "name": "Accept",
              "value": "application/json"
            },
            {
              "name": "Authorization",
              "value": "LOW myaccesskey:mysecret"
            }
          ]
        },
        "sendBody": true,
        "contentType": "form-urlencoded",
        "bodyParameters": {
          "parameters": [
            {
              "name": "url",
              "value": "=https://example.com"
            }
          ]
        },
        "options": {}
      },
      "type": "n8n-nodes-base.httpRequest",
      "typeVersion": 4.2,
      "position": [
        -20,
        -200
      ],
      "id": "aca6b759-8629-4328-a68f-785aaae5ad84",
      "name": "Web archive",
      "alwaysOutputData": false,
      "onError": "continueRegularOutput",
      "notes": "Documentation: https://docs.google.com/document/d/1Nsv52MvSjbLb2PCpHlat0gkzw0EvtSgpKHu4mk0MnrA/edit?usp=sharing"
    }
  ],
  "connections": {},
  "pinData": {}
}
```

### **Steps to Use**

1. **Import the Workflow**:
   - Copy the JSON workflow above.
   - Open your n8n instance.
   - Go to the **Workflows** page and click **Import Workflow**.
   - Paste the JSON and click **Import**.

2. **Set Up Credentials**:
   - Replace `myaccesskey` and `mysecret` in the **Authorization** header with your IA-S3 credentials.

3. **Add URL to Archive**:
   - In the `url` parameter of the `bodyParameters`,add the URL you want to archive after `=` (e.g., `=https://example.com`).

4. **Run the Workflow**:
   - Execute the workflow to archive the URL.


### **Output**
If successful, the response will include the archived URL details.

## **Additional Resources**

- [Internet Archive S3 API Documentation](https://archive.org/help/abouts3.txt)
- [n8n Documentation](https://docs.n8n.io/)

## **License**

This project is licensed under the [MIT License](LICENSE).
Feel free to contribute, report issues, or suggest improvements! 
