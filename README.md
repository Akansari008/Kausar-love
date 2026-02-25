# Kausar-love
import React, { useState, useEffect } from "react";
import { motion, AnimatePresence } from "framer-motion";
import { Heart } from "lucide-react";
import { Button } from "@/components/ui/button";
import { Card, CardContent } from "@/components/ui/card";

export default function LoveAnniversaryWebsite() {
  const [showLetter, setShowLetter] = useState(false);
  const [timeLeft, setTimeLeft] = useState({});
  const [typedText, setTypedText] = useState("");
  const [showPopup, setShowPopup] = useState(false);
  const [entered, setEntered] = useState(false);

  const fullText = "Kausar Qureshi... This is our story ❤️";

  // Typing Effect
  useEffect(() => {
    let index = 0;
    const typingInterval = setInterval(() => {
      setTypedText(fullText.slice(0, index));
      index++;
      if (index > fullText.length) clearInterval(typingInterval);
    }, 80);
    return () => clearInterval(typingInterval);
  }, []);

  // Countdown
  useEffect(() => {
    const targetDate = new Date("April 22, 2027 00:00:00").getTime();
    const interval = setInterval(() => {
      const now = new Date().getTime();
      const distance = targetDate - now;
      if (distance < 0) {
        clearInterval(interval);
        return;
      }
      setTimeLeft({
        days: Math.floor(distance / (1000 * 60 * 60 * 24)),
        hours: Math.floor((distance / (1000 * 60 * 60)) % 24),
        minutes: Math.floor((distance / 1000 / 60) % 60),
        seconds: Math.floor((distance / 1000) % 60),
      });
    }, 1000);
    return () => clearInterval(interval);
  }, []);

  if (!entered) {
    return (
      <div className="h-screen flex flex-col items-center justify-center bg-black text-white text-center p-6 relative overflow-hidden">
        {/* Heartbeat Sound */}
        <audio autoPlay loop>
          <source src="/heartbeat.mp3" type="audio/mpeg" />
        </audio>
        {/* Glowing Ring Animation */}
        <motion.div
          animate={{ scale: [1, 1.2, 1], opacity: [0.6, 1, 0.6] }}
          transition={{ duration: 2, repeat: Infinity }}
          className="absolute w-72 h-72 rounded-full border-4 border-pink-500"
        />
        <motion.h1
          initial={{ opacity: 0, scale: 0.8 }}
          animate={{ opacity: 1, scale: 1 }}
          transition={{ duration: 1.5 }}
          className="text-4xl md:text-6xl font-bold mb-8 z-10"
        >
          A Love Story Awaits...
        </motion.h1>
        <motion.p
          initial={{ opacity: 0 }}
          animate={{ opacity: 1 }}
          transition={{ delay: 1, duration: 1 }}
          className="mb-10 text-lg md:text-xl z-10"
        >
          22 April 2025 — The day everything changed ❤️
        </motion.p>
        <motion.div initial={{ opacity: 0 }} animate={{ opacity: 1 }} transition={{ delay: 2, duration: 1 }} className="z-10">
          <Button onClick={() => setEntered(true)} className="text-lg px-10 py-6 rounded-2xl shadow-2xl">
            Tap To Enter Our Story 💖
          </Button>
        </motion.div>
      </div>
    );
  }

  return (
    <div className="relative min-h-screen overflow-hidden bg-gradient-to-br from-pink-100 via-rose-50 to-purple-100 text-gray-800">
      {/* Background Music */}
      <audio autoPlay loop>
        <source src="/romantic-music.mp3" type="audio/mpeg" />
      </audio>
      {/* Floating Hearts */}
      <div className="absolute inset-0 pointer-events-none overflow-hidden">
        {[...Array(25)].map((_, i) => (
          <motion.div
            key={i}
            initial={{ y: "100%", x: Math.random() * 100 + "%", opacity: 0.6 }}
            animate={{ y: "-10%" }}
            transition={{ duration: 8 + Math.random() * 5, repeat: Infinity, delay: Math.random() * 5 }}
            className="absolute text-pink-400 text-2xl"
          >
            ❤️
          </motion.div>
        ))}
      </div>
      {/* Hero */}
      <section className="h-screen flex flex-col justify-center items-center text-center p-6">
        <h1 className="text-3xl md:text-5xl font-mono mb-6 h-16">{typedText}</h1>
        <motion.h2
          initial={{ opacity: 0, y: -40 }}
          animate={{ opacity: 1, y: 0 }}
          transition={{ duration: 1 }}
          className="text-5xl md:text-7xl font-bold mb-6"
        >
          One Year of Us ❤️
        </motion.h2>
        <p className="text-xl md:text-2xl max-w-2xl">
          From a simple "Hi" in a group chat to the most beautiful chapter of my life with Kausar Qureshi.
        </p>
      </section>
      {/* Countdown */}
      <section className="py-16 text-center bg-white/60">
        <h2 className="text-3xl font-bold mb-6">⏳ Countdown to Our Next Anniversary</h2>
        <div className="flex justify-center gap-6 text-xl font-semibold">
          <div>{timeLeft.days || 0} Days</div>
          <div>{timeLeft.hours || 0} Hours</div>
          <div>{timeLeft.minutes || 0} Minutes</div>
          <div>{timeLeft.seconds || 0} Seconds</div>
        </div>
      </section>
      {/* Proposal Button */}
      <div className="text-center py-10">
        <Button onClick={() => setShowPopup(true)} className="text-lg px-8 py-6 rounded-2xl shadow-xl">
          Click For A Surprise 💍
        </Button>
      </div>
      {/* Popup */}
      <AnimatePresence>
        {showPopup && (
          <motion.div
            initial={{ opacity: 0 }}
            animate={{ opacity: 1 }}
            exit={{ opacity: 0 }}
            className="fixed inset-0 bg-black/60 flex items-center justify-center z-50"
          >
            <motion.div
              initial={{ scale: 0.5 }}
              animate={{ scale: 1 }}
              exit={{ scale: 0.5 }}
              className="bg-white p-10 rounded-2xl text-center shadow-2xl max-w-md"
            >
              <h3 className="text-3xl font-bold mb-4">Kausar Qureshi 💖</h3>
              <p className="text-lg mb-6">
                One year down... A lifetime to go.
                Will you stay with me forever?
              </p>
              <Button onClick={() => setShowPopup(false)} className="px-6 py-4 rounded-xl">
                Yes, Always ❤️
              </Button>
            </motion.div>
          </motion.div>
        )}
      </AnimatePresence>
      <footer className="text-center py-6 text-sm text-gray-600">
        Made with endless love for Kausar Qureshi — 22 April 2026 💕
      </footer>
    </div>
  );
}
