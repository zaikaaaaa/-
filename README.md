import { useState, useEffect } from "react";
import { Card, CardContent } from "@/components/ui/card";
import { Input } from "@/components/ui/input";
import { Button } from "@/components/ui/button";

export default function MirZabytyhVeschey() {
  const [submitted, setSubmitted] = useState(false);
  const [thing, setThing] = useState("");

  useEffect(() => {
    const savedThing = localStorage.getItem("forgottenThing");
    if (savedThing) {
      setSubmitted(true);
      setThing(savedThing);
    }
  }, []);

  const handleSubmit = (e: React.FormEvent) => {
    e.preventDefault();
    localStorage.setItem("forgottenThing", thing);
    setSubmitted(true);
  };

  return (
    <div className="min-h-screen bg-gradient-to-b from-[#fdfaf6] to-[#eeeae4] text-[#2c2c2c] px-4 py-10 font-handwriting relative overflow-hidden">
      {/* Floating petals background */}
      <div className="absolute inset-0 pointer-events-none z-0 animate-background">
        <div className="absolute top-0 left-0 w-full h-full bg-[url('/petals.gif')] bg-repeat opacity-20"></div>
      </div>

      {/* Optional background music */}
      <audio autoPlay loop className="hidden">
        <source src="/bg-music.mp3" type="audio/mpeg" />
      </audio>

      <div className="max-w-3xl mx-auto space-y-12 relative z-10">
        <header className="text-center">
          <h1 className="text-5xl font-bold mb-4 tracking-tight">Мир забытых вещей</h1>
          <p className="italic text-xl text-neutral-600">
            "Ни одно моё воспоминание никогда не окажется в мире забытых вещей."
          </p>
        </header>

        <section className="space-y-6">
          <h2 className="text-2xl font-semibold">Глава первая</h2>
          <p>
            Существует мир забытых вещей. Туда попадают все предметы, о которых кто-то когда-то забыл,
            которые потеряли и так и не нашли. Они улавливают запах забвения и перестают чувствовать себя нужными…
          </p>
          <p>
            Туда попал и мой амулет, подаренный мне старым домовладельцем во время моего пребывания в Японии на
            летних каникулах. Было это двадцать пять лет назад...
          </p>
        </section>

        <section className="space-y-6">
          <h2 className="text-2xl font-semibold">Глава вторая</h2>
          <p>
            Через пару дней я вернулся в Токио. И никак не мог выбросить из головы тот день накануне возвращения.
            Каждый раз, беря в руки мешочек, я вспоминал о книге. И вспоминал о ней…
          </p>
        </section>

        <section className="space-y-6">
          <h2 className="text-2xl font-semibold">Глава третья</h2>
          <p>
            Как ни трудно догадаться, я так и не получил ответа. Ни тогда, ни неделю, ни даже месяцы и годы спустя…
          </p>
          <p>
            Ведь тогда я решил, что ни одно моё воспоминание никогда не окажется в мире забытых вещей.
          </p>
        </section>

        <section className="mt-10">
          <Card className="bg-white/80 shadow-xl p-6">
            <CardContent className="space-y-4">
              <h3 className="text-xl font-semibold">Оставьте свою забытую вещь</h3>
              {submitted ? (
                <p className="text-green-600 italic">
                  Спасибо. Ваша вещь сохранена в памяти.
                </p>
              ) : (
                <form onSubmit={handleSubmit} className="space-y-4">
                  <Input
                    placeholder="Например: красный зонт, забытый в поезде…"
                    value={thing}
                    onChange={(e) => setThing(e.target.value)}
                  />
                  <Button type="submit">Сохранить</Button>
                </form>
              )}
            </CardContent>
          </Card>
        </section>

        <footer className="text-center text-sm text-neutral-500 mt-10">
          © {new Date().getFullYear()} Мир забытых вещей. Все права забыты.
        </footer>
      </div>
    </div>
  );
}
