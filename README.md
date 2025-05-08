# D-C-interact-
Dushanbe City interact 
import React, { useState } from "react";
import axios from "axios";

export default function Home() {
  const [form, setForm] = useState({ name: "", phone: "", telegram: "" });
  const [sent, setSent] = useState(false);

  const sendTelegram = async () => {
    const token = "7552079979:AAHjrEM6zzEvsHwnt38_WWfBc4XghD019lY";
    const chatId = "@your_username_or_chat_id"; // заменим на ID позже
    const message = `\uD83C\uDFE2 Заявка с сайта Dar&Shahr Properties\n\nИмя: ${form.name}\nТелефон: ${form.phone}\nTelegram: ${form.telegram}`;

    await axios.post(`https://api.telegram.org/bot${token}/sendMessage`, {
      chat_id: chatId,
      text: message,
    });

    setSent(true);
  };

  const handleSubmit = (e) => {
    e.preventDefault();
    sendTelegram();
  };

  return (
    <div className="min-h-screen bg-gray-50 flex flex-col items-center justify-center p-6">
      <img src="/logo.png" alt="Dar&Shahr Properties" className="w-56 mb-6" />
      <h1 className="text-3xl font-bold mb-4 text-gray-800">Апартаменты в Дубае от $250 000</h1>

      {!sent ? (
        <form
          onSubmit={handleSubmit}
          className="bg-white p-6 rounded-2xl shadow-lg w-full max-w-md"
        >
          <label className="block mb-2 font-medium">Имя</label>
          <input
            type="text"
            value={form.name}
            onChange={(e) => setForm({ ...form, name: e.target.value })}
            className="border p-2 w-full mb-4 rounded-lg"
            required
          />

          <label className="block mb-2 font-medium">Телефон</label>
          <input
            type="text"
            value={form.phone}
            onChange={(e) => setForm({ ...form, phone: e.target.value })}
            className="border p-2 w-full mb-4 rounded-lg"
            required
          />

          <label className="block mb-2 font-medium">Telegram</label>
          <input
            type="text"
            value={form.telegram}
            onChange={(e) => setForm({ ...form, telegram: e.target.value })}
            className="border p-2 w-full mb-4 rounded-lg"
            required
          />

          <button
            type="submit"
            className="bg-blue-600 text-white py-2 px-4 rounded-xl hover:bg-blue-700"
          >
            Отправить заявку
          </button>
        </form>
      ) : (
        <div className="text-green-600 text-lg font-semibold">
          Ваша заявка успешно отправлена!
        </div>
      )}
    </div>
  );
}
