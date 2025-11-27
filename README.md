<!DOCTYPE html>
<html>
<head>
  <meta charset="UTF-8" />
  <title>Agentforce Test</title>
</head>
<body>

  <h2>Test Your Salesforce Agentforce Service Agent</h2>

  <input id="msg" placeholder="Type message…" style="width:250px;" />
  <button onclick="send()">Send</button>

  <div id="response" style="margin-top:20px; font-family:Arial;"></div>

  <script>
    async function send() {
      const userText = document.getElementById("msg").value;
      document.getElementById("response").innerHTML = "Sending...";

      // -------------------------------------------------------
      // 🔴 REPLACE THESE TWO VALUES WITH YOUR AGENTFORCE DETAILS
      const ENDPOINT = "https://YOUR_AGENTFORCE_ENDPOINT_HERE"; 
      const AGENT_ID = "YOUR_AGENT_ID_HERE";                     
      // -------------------------------------------------------

      const body = {
        agentId: AGENT_ID,
        input: userText
      };

      try {
        const res = await fetch(ENDPOINT, {
          method: "POST",
          headers: {
            "Content-Type": "application/json"
          },
          body: JSON.stringify(body)
        });

        const data = await res.json();
        document.getElementById("response").innerHTML =
          "<strong>Agent:</strong> " + (data.output?.text || JSON.stringify(data));
      } 
      catch (err) {
        document.getElementById("response").innerHTML =
          "Error: " + err.message;
      }
    }
  </script>

</body>
</html>
