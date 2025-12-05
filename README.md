# 📬 Contact Form Workflow (n8n)

Dies ist mein n8n Workflow für ein Kontaktformular, das über meine Website eine Nachricht an meinen Telegram-Chat sendet.

Der Workflow nimmt eingehende Formulardaten über einen Webhook entgegen, prüft sie im Code-Node und sendet anschließend eine Telegrampnachricht.

---

## 🚀 Funktionen

- Empfängt Formulardaten via **POST Webhook**
- Validiert:
  - Name
  - Email
  - Message
- Erstellt automatisch eine formatierte Nachricht
- Sendet die Nachricht an Telegram

---

## 📤 Workflow importieren

1. n8n öffnen  
2. **Import from File**  
3. Datei auswählen:  
   ```bash
   workflows/contact-form.json
