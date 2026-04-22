<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Voucher Life Chatbot</title>
    <style>
        body { font-family: Arial, sans-serif; }
        #chatbot { width: 300px; height: 400px; border: 1px solid #ccc; overflow: auto; padding: 10px; position: relative; }
        #user-input { position: absolute; bottom: 10px; width: calc(100% - 22px); }
    </style>
</head>
<body>
    <div id="chatbot"></div>
    <input type="text" id="user-input" placeholder="Type your message..." />
    <script>
        const chatbot = document.getElementById('chatbot');
        const userInput = document.getElementById('user-input');
        const knowledgeBase = {
            en: {
                greeting: "Hello! How can I assist you today?",
                farewell: "Goodbye! Have a great day!",
                help: "You can ask me about vouchers, discounts, and more!"
            },
            ar: {
                greeting: "مرحبا! كيف يمكنني مساعدتك اليوم؟",
                farewell: "مع السلامة! أتمنى لك يومًا سعيدًا!",
                help: "يمكنك أن تسألني عن القسائم، والخصومات، وأكثر!"
            }
        };
        let currentLanguage = 'en';

        function respondToUser(input) {
            const lowerInput = input.toLowerCase();
            let response = '';  
            if (lowerInput.includes('hello')) {
                response = knowledgeBase[currentLanguage].greeting;
            } else if (lowerInput.includes('bye')) {
                response = knowledgeBase[currentLanguage].farewell;
            } else if (lowerInput.includes('help')) {
                response = knowledgeBase[currentLanguage].help;
            } else {
                response = currentLanguage === 'en' ? "I'm sorry, I don't understand." : "عذرًا، لا أفهم.";
            }
            chatbot.innerHTML += '<div>' + response + '</div>';
            chatbot.scrollTop = chatbot.scrollHeight;
        }

        userInput.addEventListener('keypress', function (e) {
            if (e.key === 'Enter') {
                const userMessage = userInput.value;
                chatbot.innerHTML += '<div><strong>You:</strong> ' + userMessage + '</div>';
                respondToUser(userMessage);
                userInput.value = '';
            }
        });
    </script>
</body>
</html>
