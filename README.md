# ashutosh0519.github.io

    box-shadow: 0px 2px 5px rgba(0, 0, 0, 0.1);
}

.suggestion-button:hover {
    background-color: #007bff;
    color: #ffffff;
}


.chatbot-footer .voice-button {
    padding: 0;
    border: none;
    border-radius: 50%;
    background-color: #25D366; 
    width: 40px;
    height: 40px;
    display: flex;
    justify-content: center;
    align-items: center;
    cursor: pointer;
    margin-right: 10px; 
    transition: all 0.3s ease;
}

.chatbot-footer .voice-button:hover {
    background-color: #20b858; 
}

.chatbot-footer .voice-button svg {
    fill: white;
    width: 24px;
    height: 24px;
}




//javascript code:

function sendMessage() {
    const userInput = document.getElementById('user-input').value.trim();
    if (userInput) {
        appendUserMessage(userInput);
        generateBotResponse(userInput);
        document.getElementById('user-input').value = '';
    }
}

function startVoiceRecognition() {
    if ('webkitSpeechRecognition' in window) {
        const recognition = new webkitSpeechRecognition();
        recognition.lang = 'en-US';
        recognition.interimResults = false;
        recognition.maxAlternatives = 1;

        recognition.start();

        recognition.onresult = function(event) {
            const userVoiceInput = event.results[0][0].transcript;
            document.getElementById('user-input').value = userVoiceInput;
            sendMessage(); // Automatically send the recognized text
        };

        recognition.onerror = function(event) {
            console.error('Speech recognition error', event.error);
        };

        recognition.onspeechend = function() {
            recognition.stop();
        };
    } else {
        alert('Your browser does not support speech recognition. Please use a different browser.');
    }
}

function appendUserMessage(message) {
    const chatBody = document.querySelector('.chatbot-body');
    const userMessage = document.createElement('div');
    console.log(userMessage);
    console.log(chatBody);
    userMessage.className = 'chat-message user-message';
    userMessage.textContent = message;
    chatBody.appendChild(userMessage);
    scrollToBottom();
}

function generateBotResponse(userInput) {
    let botMessageText = '';
    const normalizedInput = userInput.toLowerCase().trim();

    const responses = {
        'tell me about diwali': 'Diwali, also known as the Festival of Lights, is one of the most popular Hindu festivals celebrated with great enthusiasm in India.',
        'holi': 'Holi is a vibrant festival of colors celebrated in India, marking the arrival of spring and the victory of good over evil.',
        'independence day': 'Independence Day in India is celebrated on August 15th each year, marking the end of British rule in 1947.',
        'yoga': 'Yoga is an ancient practice from India that promotes physical, mental, and spiritual well-being.',
        'taj mahal': 'The Taj Mahal is an iconic white marble mausoleum in Agra, India, built by Mughal Emperor Shah Jahan in memory of his wife Mumtaz Mahal.',
        'mahatma gandhi': 'Mahatma Gandhi was a leader of India\'s non-violent independence movement against British rule, and he is known as the Father of the Nation.',
        'kathak': 'Kathak is one of the eight classical dances of India, originating from the northern regions and characterized by intricate footwork and expressive gestures.',
        'sanskrit': 'Sanskrit is an ancient Indian language and the liturgical language of Hinduism, Buddhism, and Jainism, known for its rich literary tradition.',
        'ganesh chaturthi': 'Ganesh Chaturthi is a Hindu festival celebrating the birth of Lord Ganesha, the elephant-headed god of wisdom and prosperity.',
        'ayurveda': 'Ayurveda is an ancient Indian system of medicine that focuses on holistic health, balancing the mind, body, and spirit through natural remedies.',
        'cricket': 'Cricket is the most popular sport in India, with a massive following and a rich history, especially known for legendary players like Sachin Tendulkar.',
        'tell me about indians' : 'Indians are the people of India, a diverse and culturally rich country in South Asia.',
        'who build you' : 'To build me! , I have Amit Kumar Sahu,Sanskar kesharwani,Tarang koshti,Sneha , uday jhariya and ashutosh tiwari.',
        'hello': 'Hello How can I help?',
        'distance between jammu and kerala' : 'The distance between jammu and kerala is 3,284 kilo metres',
        'sari' : 'The sari is a traditional garment worn by women in India. It is a long piece of cloth, usually about 6 to 9 yards in length, draped elegantly around the body. The sari is not just a piece of clothing but a symbol of grace, beauty, and cultural heritage. Different regions in India have their own unique styles of draping a sari, reflecting the diversity of Indian culture.',
        'namaste' : 'Namaste is a traditional Indian greeting, which means "I bow to you." The word is derived from Sanskrit and is often accompanied by a slight bow made with hands pressed together, palms touching and fingers pointing upwards, thumbs close to the chest. It signifies respect, reverence, and acknowledgment of the divine in others.',
        'capital of bhopal' : 'The Capital of madhya pradesh is bhopal',
        'capital of india' : 'The capital of India is New Delhi',

    };

  
    for (const keyword in responses) {
        if (normalizedInput.includes(keyword)) {
            botMessageText = responses[keyword];
            break;
        }
    }

  
    if (!botMessageText) {
        botMessageText = 'Sorry, I am not sure about that. Can you please ask something else related to Indian culture?';
    }

    appendBotMessage(botMessageText);
}

    



function appendBotMessage(message) {
    const chatBody = document.querySelector('.chatbot-body');
    const botMessage = document.createElement('div');
    botMessage.className = 'chat-message bot-message';
    botMessage.textContent = message;
    chatBody.appendChild(botMessage);
    speak(message);
    scrollToBottom();
}


function handleSuggestionClick(suggestion) {
    document.getElementById('user-input').value = suggestion;
    sendMessage();
}


function speak(text) {
    const utterance = new SpeechSynthesisUtterance(text);
    window.speechSynthesis.speak(utterance);
}


function scrollToBottom() {
    const chatBody = document.querySelector('.chatbot-body');
    chatBody.scrollTop = chatBody.scrollHeight;
}
