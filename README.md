# gut-friendly-wellness
A modern health‑tech inspired web app designed to support people with food intolerances (including lactose intolerance), common food allergies, and acid reflux. 
import { useState } from "react";
import { Card, CardContent } from "@/components/ui/card";
import { Button } from "@/components/ui/button";
import { Input } from "@/components/ui/input";
import { Checkbox } from "@/components/ui/checkbox";
import { motion } from "framer-motion";
import { HeartPulse, Salad, Dumbbell, Calendar, Search, Sun, Moon } from "lucide-react";

export default function GutFriendlyWellness() {
  const [activeTab, setActiveTab] = useState("home");
  const [checkerInput, setCheckerInput] = useState("");
  const [darkMode, setDarkMode] = useState(true);

  const [filters, setFilters] = useState({
    lactoseFree: true,
    glutenFree: false,
    nutFree: false,
    refluxSafe: true,
    vegan: false,
    halal: false,
    lowFodmap: false,
  });

  const meals = [
    { name: "Oatmeal with Banana & Chia", tags: ["lactoseFree", "refluxSafe", "vegan"] },
    { name: "Grilled Chicken & Quinoa Bowl", tags: ["glutenFree", "lactoseFree", "halal"] },
    { name: "Baked Salmon with Sweet Potato", tags: ["refluxSafe", "nutFree"] },
    { name: "Tofu & Rice Stir Fry", tags: ["vegan", "lowFodmap", "lactoseFree"] },
  ];

  const exercises = [
    { day: "Monday", name: "Low-impact walking", note: "Supports digestion" },
    { day: "Wednesday", name: "Upper body strength", note: "Avoid post-meal workouts" },
    { day: "Friday", name: "Yoga (reflux-safe)", note: "No inversions" },
  ];

  const refluxTriggers = ["tomato", "coffee", "chocolate", "spicy", "fried", "alcohol", "citrus"];

  const isRefluxSafe = checkerInput
    ? !refluxTriggers.some((t) => checkerInput.toLowerCase().includes(t))
    : null;

  const filteredMeals = meals.filter((meal) =>
    Object.keys(filters).every((f) => !filters[f] || meal.tags.includes(f))
  );

  const themeClasses = darkMode
    ? "bg-gradient-to-br from-neutral-950 via-slate-900 to-emerald-950 text-white"
    : "bg-gradient-to-br from-emerald-50 via-sky-50 to-indigo-50 text-neutral-900";

  return (
    <div className={`min-h-screen p-6 transition-colors duration-300 ${themeClasses}`}>
      <div className="flex justify-between items-center max-w-6xl mx-auto mb-6">
        <motion.h1 initial={{ opacity: 0 }} animate={{ opacity: 1 }} className="text-4xl font-bold">
          Gut-Friendly Wellness
        </motion.h1>
        <Button variant="outline" onClick={() => setDarkMode(!darkMode)}>
          {darkMode ? <Sun /> : <Moon />}
        </Button>
      </div>

      {/* App Navigation */}
      <div className="flex justify-center gap-3 mb-10">
        {["home", "planner", "checker"].map((tab) => (
          <Button
            key={tab}
            className="capitalize"
            variant={activeTab === tab ? "default" : "outline"}
            onClick={() => setActiveTab(tab)}
          >
            {tab}
          </Button>
        ))}
      </div>

      {/* HOME */}
      {activeTab === "home" && (
        <div className="grid md:grid-cols-2 gap-6 max-w-6xl mx-auto">
          <Card className="rounded-2xl backdrop-blur bg-white/5">
            <CardContent className="p-4">
              <h2 className="text-xl font-semibold flex items-center gap-2 mb-4"><Salad /> Dietary Filters</h2>
              {Object.keys(filters).map((f) => (
                <label key={f} className="flex items-center gap-2 mb-2">
                  <Checkbox checked={filters[f]} onCheckedChange={(v) => setFilters({ ...filters, [f]: v })} />
                  <span className="capitalize">{f.replace(/([A-Z])/g, " $1")}</span>
                </label>
              ))}
            </CardContent>
          </Card>

          <Card className="rounded-2xl backdrop-blur bg-white/5">
            <CardContent className="p-4">
              <h2 className="text-xl font-semibold flex items-center gap-2 mb-4"><HeartPulse /> Reflux Guidance</h2>
              <ul className="list-disc ml-4 text-gray-300 space-y-1">
                <li>Smaller meals, spaced evenly</li>
                <li>No lying down within 2 hours</li>
                <li>Train upright where possible</li>
                <li>Track personal trigger foods</li>
              </ul>
            </CardContent>
          </Card>
        </div>
      )}

      {/* PLANNER */}
      {activeTab === "planner" && (
        <div className="max-w-6xl mx-auto grid md:grid-cols-2 gap-6">
          <Card className="rounded-2xl backdrop-blur bg-white/5">
            <CardContent className="p-4">
              <h2 className="text-xl font-semibold flex items-center gap-2 mb-4"><Calendar /> Weekly Meal Plan</h2>
              {filteredMeals.map((meal) => (
                <div key={meal.name} className="p-3 border border-white/10 rounded-xl mb-2">
                  {meal.name}
                </div>
              ))}
            </CardContent>
          </Card>

          <Card className="rounded-2xl backdrop-blur bg-white/5">
            <CardContent className="p-4">
              <h2 className="text-xl font-semibold flex items-center gap-2 mb-4"><Dumbbell /> Weekly Workout Plan</h2>
              {exercises.map((ex) => (
                <div key={ex.day} className="p-3 border border-white/10 rounded-xl mb-2">
                  <p className="font-medium">{ex.day}: {ex.name}</p>
                  <p className="text-sm text-gray-400">{ex.note}</p>
                </div>
              ))}
            </CardContent>
          </Card>
        </div>
      )}

      {/* CHECKER */}
      {activeTab === "checker" && (
        <div className="max-w-xl mx-auto">
          <Card className="rounded-2xl backdrop-blur bg-white/5">
            <CardContent className="p-4">
              <h2 className="text-xl font-semibold flex items-center gap-2 mb-4"><Search /> Reflux Safety Checker</h2>
              <Input
                placeholder="Enter a food or ingredient (e.g. tomato pasta)"
                value={checkerInput}
                onChange={(e) => setCheckerInput(e.target.value)}
              />
              {isRefluxSafe !== null && (
                <p className={`mt-4 font-medium ${isRefluxSafe ? "text-emerald-400" : "text-rose-400"}`}>
                  {isRefluxSafe ? "Likely reflux-safe" : "May trigger acid reflux"}
                </p>
              )}
            </CardContent>
          </Card>
        </div>
      )}

      <footer className="text-center text-sm text-gray-400 mt-12">
        Portfolio project · Modern health-tech UI
      </footer>
    </div>
  );
}
