// EduFace - Site educacional estilo Facebook // Estrutura inicial com React + TailwindCSS

import { useState } from 'react'; import { Button } from "@/components/ui/button";

export default function EduFace() { const [input, setInput] = useState(""); const [chatLog, setChatLog] = useState([]);

const handleSend = () => { if (!input) return; setChatLog([...chatLog, { type: 'user', text: input }]); // Aqui é onde a chamada à API do ChatGPT será integrada setInput(""); };

return ( <div className="flex h-screen bg-gray-100"> {/* Sidebar esquerda */} <aside className="w-1/5 bg-white shadow p-4"> <h2 className="text-xl font-bold mb-4">EduFace</h2> <nav className="space-y-2"> <a href="#" className="block text-blue-600 font-semibold">Criador de Trabalhos</a> <a href="#" className="block">Biblioteca PDF</a> <a href="#" className="block">Chat com Tutor</a> <a href="#" className="block">Configurações</a> </nav> </aside>

{/* Feed principal */}
  <main className="flex-1 p-6 overflow-y-auto">
    <h1 className="text-2xl font-bold mb-4">Criador de Trabalhos Estudantis</h1>
    <textarea
      className="w-full h-40 p-2 border border-gray-300 rounded mb-4"
      placeholder="Digite seu trabalho aqui..."
    ></textarea>
    <div className="flex gap-2">
      <Button>Salvar como PDF</Button>
      <Button variant="outline">Gerar Sugestão com IA</Button>
    </div>

    <hr className="my-8" />

    <h2 className="text-xl font-bold mb-2">Chat com o SeedBot</h2>
    <div className="bg-white p-4 border rounded h-64 overflow-y-auto">
      {chatLog.map((msg, index) => (
        <div key={index} className={`mb-2 ${msg.type === 'user' ? 'text-right' : 'text-left'}`}>
          <span className="inline-block bg-blue-100 p-2 rounded max-w-xs">
            {msg.text}
          </span>
        </div>
      ))}
    </div>
    <div className="mt-4 flex">
      <input
        value={input}
        onChange={(e) => setInput(e.target.value)}
        placeholder="Pergunte algo ao SeedBot..."
        className="flex-1 border p-2 rounded-l"
      />
      <button
        onClick={handleSend}
        className="bg-blue-600 text-white px-4 rounded-r"
      >
        Enviar
      </button>
    </div>
  </main>

  {/* Sidebar direita */}
  <aside className="w-1/5 bg-white shadow p-4">
    <h2 className="text-lg font-semibold mb-2">Dicas Rápidas</h2>
    <ul className="text-sm space-y-1">
      <li>• Use títulos claros</li>
      <li>• Citações fortalecem o texto</li>
      <li>• Revise antes de salvar</li>
    </ul>
  </aside>
</div>

); }

/* README.md para EduFace

EduFace é uma plataforma educacional moderna com design inspirado no Facebook, feita para estudantes criarem trabalhos, salvarem PDFs e interagirem com um chatbot educacional usando a API do ChatGPT.

Funcionalidades

Criador de trabalhos estudantis

Geração e download de PDFs

Chatbot SeedBot com inteligência artificial

Layout intuitivo estilo rede social

Dicas rápidas e progressos à direita


Tecnologias Utilizadas

React.js

Tailwind CSS

OpenAI API (ChatGPT)

(Opcional) Firebase para autenticação e banco de dados


Como Rodar Localmente

# Clone o projeto
https://github.com/seuusuario/eduface.git
cd eduface

# Instale as dependências
npm install

# Inicie o servidor local
npm run dev

Integração com ChatGPT

Dentro da função handleSend, insira a chamada à API da OpenAI com sua chave de acesso:

fetch('https://api.openai.com/v1/chat/completions', {
  method: 'POST',
  headers: {
    'Content-Type': 'application/json',
    'Authorization': `Bearer SUA_CHAVE_API`
  },
  body: JSON.stringify({
    model: 'gpt-3.5-turbo',
    messages: [{ role: 'user', content: input }]
  })
})
.then(res => res.json())
.then(data => {
  const reply = data.choices[0].message.content;
  setChatLog([...chatLog, { type: 'bot', text: reply }]);
});

Licença

Este projeto é open-source sob a licença MIT. */

