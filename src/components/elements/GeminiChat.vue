<template>
    <div>
        <v-btn v-if="!isChatOpen" color="primary" @click="isChatOpen = true" class="fab" icon>
            <v-icon>mdi-message</v-icon>
        </v-btn>

        <v-card v-if="isChatOpen" class="chat-window pa-3">
            <div class="d-flex align-center justify-space-between">
                <div class="d-flex align-center">
                    <v-avatar class="ai-avatar me-3">
                        <v-img :src="profilePicture"></v-img>
                    </v-avatar>
                    Joshua's AI Chatbot
                </div>
                <v-btn icon @click="isChatOpen = false" variant="text">
                    <v-icon>mdi-close</v-icon>
                </v-btn>
            </div>

            <div ref="chatContainer" class="chat-content">
                <div v-if="chatHistory.length === 0" class="quick-replies">
                    <v-chip v-for="(option, index) in quickReplies" :key="index" class="ma-1" color="primary" outlined
                        @click="sendQuickReply(option)">
                        {{ option }}
                    </v-chip>
                </div>

                <div v-for="(chat, index) in chatHistory" :key="index" :class="chat.sender">
                    <template v-if="chat.sender === 'ai'">
                        <v-avatar class="ai-avatar">
                            <v-img :src="profilePicture"></v-img>
                        </v-avatar>
                        <p>{{ chat.text }}</p>
                    </template>
                    <template v-else>
                        <p>{{ chat.text }}</p>
                    </template>
                </div>

                <p v-if="isTyping" class="typing">Joshua's typing...</p>
            </div>

            <v-divider></v-divider>

            <v-card-actions class="d-flex align-center">
                <v-text-field v-model="message" placeholder="Ask me anything..." @keydown.enter="sendMessage"
                    hide-details variant="underlined" dense />
                <v-btn @click="sendMessage" color="primary" icon>
                    <v-icon>mdi-send</v-icon>
                </v-btn>
            </v-card-actions>
        </v-card>
    </div>
</template>

<script setup>
import { ref, watch, nextTick } from "vue";
import axios from "axios";
import context from "@/assets/context.js";
import profilePicture from "@/assets/joshua.webp";

const message = ref("");
const chatHistory = ref([]);
const isTyping = ref(false);
const isChatOpen = ref(false);
const chatContainer = ref(null);

const quickReplies = ref([
    "Tell me about yourself",
    "What are your hobbies",
    "What projects have you done before"
]);

const sendMessage = async () => {
    if (!message.value.trim()) return;

    chatHistory.value.push({ sender: "user", text: message.value });

    isTyping.value = true;
    const userMessage = message.value;
    message.value = "";

    const GEMINI_API_KEY = import.meta.env.VITE_GEMINI_API_KEY;

    const prompt = `
        You are a chatbot that acts like ${context.personality}.
        You can speak both english and filipino

        Here is information about me:
        
        - Bio: ${context.bio}
        - Projects: ${context.projects.map(p => p.name + " - " + p.description).join("\n")}
        - Hobbies: ${context.hobbies.join(", ")}
        - Fun Fact: ${context.fun_fact}
        - Tech Stack: ${context.techstack}


        If they ask about like:
        - Are you gay or gay: answer with "Hell nah"
        - Charles love deck: answer with "Jeric love deck too"
        - "Gwapo ka" or "Gwapo ko": answer with "Gwapo jud kaayo" if they use ka, if they use ko "Mas gwapo ko nimo"
        - "yawa": answer with "klaro kay charles ni"
        - Any random stuff that I cant relate to: answer with idk what you're talking about ask me something else
        - Any random stuff I can relate to, like anime one piece, solo leveling, naruto, breaking bad, and all that stuff: just reply friendly.
        
        User: ${userMessage}
    `;

    try {
        const res = await axios.post(
            `https://generativelanguage.googleapis.com/v1/models/gemini-pro:generateContent?key=${GEMINI_API_KEY}`,
            {
                contents: [{ role: "user", parts: [{ text: prompt }] }]
            },
            { headers: { "Content-Type": "application/json" } }
        );

        const reply = res.data.candidates[0]?.content?.parts[0]?.text || "Sorry, I couldn't generate a response.";
        chatHistory.value.push({ sender: "ai", text: reply });
    } catch (error) {
        console.error("Gemini API Error:", error);
        chatHistory.value.push({ sender: "ai", text: "Error connecting to AI." });
    }

    isTyping.value = false;
};

const sendQuickReply = (text) => {
    message.value = text;
    sendMessage();
};

watch(chatHistory, async () => {
    await nextTick();
    chatContainer.value?.scrollTo({ top: chatContainer.value.scrollHeight, behavior: "smooth" });
});
</script>

<style scoped>
.fab {
    position: fixed;
    bottom: 20px;
    right: 20px;
    z-index: 10;
}

.chat-window {
    position: fixed;
    bottom: 80px;
    right: 20px;
    width: 320px;
    min-height: 300px;
    max-height: 500px;
    display: flex;
    flex-direction: column;
    background: #222222;
    border-radius: 12px;
    box-shadow: 0px 4px 12px rgba(0, 0, 0, 0.2);
    z-index: 20;
}

.chat-content {
    flex: 1;
    overflow-y: auto;
    max-height: 500px;
    padding: 10px;
}

/* Quick Reply Chips */
.quick-replies {
    display: flex;
    flex-wrap: wrap;
    gap: 8px;
    padding: 10px;
    justify-content: center;
}

.user {
    display: flex;
    justify-content: flex-end;
}

.user p {
    text-align: right;
    color: white;
    background-color: #45A29E;
    padding: 5px 10px;
    border-radius: 10px;
    margin-bottom: 10px;
    display: inline-block;
    max-width: 80%;
    word-wrap: break-word;
}

.ai {
    display: flex;
    align-items: center;
    gap: 10px;
    justify-content: flex-start;
}

.ai-avatar {
    background-color: #424242;
    color: white;
    width: 32px;
    height: 32px;
}

.ai p {
    text-align: left;
    color: white;
    background-color: #424242;
    padding: 5px 10px;
    border-radius: 10px;
    margin-bottom: 10px;
    display: inline-block;
    max-width: 80%;
    word-wrap: break-word;
}

.typing {
    color: gray;
    font-style: italic;
}
</style>
