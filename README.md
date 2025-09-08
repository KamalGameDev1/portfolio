import React, { useMemo, useState } from "react";
import { motion } from "framer-motion";
import { Github, Linkedin, Mail, Globe, Download, Gamepad2, Search, Filter, Smartphone, Monitor, ChevronRight } from "lucide-react";

// =============================
// Data — edit these to your info
// =============================
const PROFILE = {
  name: "Kamal Saini",
  title: "Unity Game Developer",
  subtitle: "2D/3D • C# • Clean Architecture • UI/UX",
  location: "Jaipur, India",
  email: "your.email@example.com",
  github: "https://github.com/your-username",
  linkedin: "https://www.linkedin.com/in/your-profile/",
  itch: "https://your-itch-username.itch.io/",
  resumeUrl: "#", // add a link to your PDF resume
};

const PROJECTS = [
  {
    id: "ludo",
    title: "Ludo (Unity)",
    summary:
      "Multiplayer Ludo with turn system, dice logic, safe cells, and win conditions.",
    details:
      "Designed modular rules, turn-queue, and UI states. Optional online-ready architecture.",
    tags: ["Unity", "C#", "Turn-Based", "UI"],
    platforms: ["Mobile", "Desktop"],
    image:
      "https://images.unsplash.com/photo-1610890716171-6b1bb98e5b1b?q=80&w=1200&auto=format&fit=crop",
    repo: "https://github.com/your-username/ludo-unity",
    demo: "https://your-itch-username.itch.io/ludo",
  },
  {
    id: "snake2d",
    title: "Snake 2D (Unity)",
    summary:
      "Classic Snake with object pooling, grid movement, and score/hi-score persistence.",
    details:
      "Lightweight architecture using ScriptableObjects for settings and events.",
    tags: ["Unity", "2D", "Object Pooling"],
    platforms: ["Mobile", "Web"],
    image:
      "https://images.unsplash.com/photo-1545289414-1c3cb1c06238?q=80&w=1200&auto=format&fit=crop",
    repo: "https://github.com/your-username/snake-2d",
    demo: "https://your-itch-username.itch.io/snake",
  },
  {
    id: "platformer2d",
    title: "2D Platformer (Unity)",
    summary:
      "Side-scroller with tilemap, coyote-time jumps, enemies, collectibles, and animations.",
    details:
      "Custom character controller, state machine, and camera parallax layers.",
    tags: ["Unity", "2D", "Animation"],
    platforms: ["Desktop", "Web"],
    image:
      "https://images.unsplash.com/photo-1546443046-ed1ce6ffd1b7?q=80&w=1200&auto=format&fit=crop",
    repo: "https://github.com/your-username/2d-platformer",
    demo: "https://your-itch-username.itch.io/platformer",
  },
  {
    id: "rolling3d",
    title: "3D Rolling Ball (Unity)",
    summary:
      "Physics-based obstacle course with checkpoints, collectibles, and timer.",
    details:
      "Rigidbody tuning, camera follow rig, and modular obstacle prefabs.",
    tags: ["Unity", "3D", "Physics"],
    platforms: ["Desktop", "Web"],
    image:
      "https://images.unsplash.com/photo-1515626655849-1a48f2023e88?q=80&w=1200&auto=format&fit=crop",
    repo: "https://github.com/your-username/3d-rolling-ball",
    demo: "https://your-itch-username.itch.io/rolling-ball",
  },
  {
    id: "turncpp",
    title: "Turn-Based Game (C++)",
    summary:
      "Grid-based tactics prototype in pure C++ with turns, actions, and pathfinding.",
    details:
      "Showcases OOP, data structures, and a minimal ECS-style loop.",
    tags: ["C++", "Turn-Based", "OOP"],
    platforms: ["Desktop"],
    image:
      "https://images.unsplash.com/photo-1535320903710-d993d3d77d29?q=80&w=1200&auto=format&fit=crop",
    repo: "https://github.com/your-username/turn-based-cpp",
    demo: "#",
  },
];

const TAGS = [
  "All",
  "Unity",
  "2D",
  "3D",
  "C#",
  "C++",
  "Turn-Based",
  "Physics",
  "UI",
  "Object Pooling",
  "Animation",
];

// =============================
// UI Helpers
// =============================
function classNames(...args) {
  return args.filter(Boolean).join(" ");
}

function IconPlatform({ p }) {
  if (p === "Mobile") return <Smartphone className="w-4 h-4" aria-label="Mobile" />;
  return <Monitor className="w-4 h-4" aria-label="Desktop/Web" />;
}

// =============================
// Components
// =============================
function ProjectCard({ p }) {
  return (
    <motion.article
      layout
      initial={{ opacity: 0, y: 20 }}
      whileInView={{ opacity: 1, y: 0 }}
      viewport={{ once: true, amount: 0.2 }}
      transition={{ type: "spring", stiffness: 80, damping: 14 }}
      className="group rounded-2xl bg-white/70 dark:bg-zinc-900/60 backdrop-blur shadow-sm ring-1 ring-zinc-200/60 dark:ring-zinc-800 overflow-hidden hover:shadow-lg hover:ring-zinc-300 transition"
    >
      <div className="relative aspect-[16/9] overflow-hidden">
        <img
          src={p.image}
          alt={p.title}
          className="h-full w-full object-cover group-hover:scale-105 transition duration-500"
          loading="lazy"
        />
        <div className="absolute inset-0 bg-gradient-to-t from-black/50 to-transparent opacity-0 group-hover:opacity-100 transition" />
        <div className="absolute top-3 left-3 flex gap-2">
          {p.platforms.map((pp) => (
            <span
              key={pp}
              className="inline-flex items-center gap-1 rounded-full bg-white/90 dark:bg-black/60 px-2 py-1 text-[10px] font-medium ring-1 ring-zinc-200 dark:ring-zinc-800"
            >
              <IconPlatform p={pp} /> {pp}
            </span>
          ))}
        </div>
      </div>
      <div className="p-4 md:p-5">
        <h3 className="text-lg md:text-xl font-semibold text-zinc-900 dark:text-zinc-100 flex items-center gap-2">
          <Gamepad2 className="w-5 h-5" /> {p.title}
        </h3>
        <p className="mt-2 text-sm text-zinc-600 dark:text-zinc-300">{p.summary}</p>
        <p className="mt-2 text-xs text-zinc-500 dark:text-zinc-400">{p.details}</p>
        <div className="mt-3 flex flex-wrap gap-2">
          {p.tags.map((t) => (
            <span key={t} className="rounded-full bg-zinc-100 dark:bg-zinc-800 px-2.5 py-1 text-xs text-zinc-700 dark:text-zinc-200 ring-1 ring-zinc-200 dark:ring-zinc-700">
              {t}
            </span>
          ))}
        </div>
        <div className="mt-4 flex items-center gap-3">
          <a
            href={p.demo}
            target="_blank"
            rel="noreferrer"
            className="inline-flex items-center gap-1.5 rounded-xl bg-zinc-900 text-white dark:bg-white dark:text-zinc-900 px-3 py-2 text-sm font-medium hover:opacity-90"
          >
            <Globe className="w-4 h-4" /> Live Demo
          </a>
          <a
            href={p.repo}
            target="_blank"
            rel="noreferrer"
            className="inline-flex items-center gap-1.5 rounded-xl ring-1 ring-zinc-300 dark:ring-zinc-700 px-3 py-2 text-sm font-medium hover:bg-zinc-100 dark:hover:bg-zinc-800"
          >
            <Github className="w-4 h-4" /> Code
          </a>
        </div>
      </div>
    </motion.article>
  );
}

export default function Portfolio() {
  const [query, setQuery] = useState("");
  const [activeTag, setActiveTag] = useState("All");

  const filtered = useMemo(() => {
    const q = query.trim().toLowerCase();
    return PROJECTS.filter((p) => {
      const matchText = `${p.title} ${p.summary} ${p.details} ${p.tags.join(" ")}`.toLowerCase();
      const tagOk = activeTag === "All" || p.tags.includes(activeTag);
      return (!q || matchText.includes(q)) && tagOk;
    });
  }, [query, activeTag]);

  return (
    <div className="min-h-screen bg-gradient-to-br from-zinc-50 via-white to-zinc-100 dark:from-zinc-950 dark:via-zinc-950 dark:to-black text-zinc-900 dark:text-zinc-100">
      {/* Nav */}
      <header className="sticky top-0 z-40 backdrop-blur bg-white/60 dark:bg-black/40 border-b border-zinc-200/60 dark:border-zinc-800">
        <div className="mx-auto max-w-6xl px-4 py-3 flex items-center justify-between">
          <a href="#home" className="font-semibold tracking-tight">Kamal Saini</a>
          <nav className="hidden md:flex items-center gap-6 text-sm">
            <a href="#projects" className="hover:opacity-80">Projects</a>
            <a href="#about" className="hover:opacity-80">About</a>
            <a href="#contact" className="hover:opacity-80">Contact</a>
            <a href={PROFILE.resumeUrl} className="inline-flex items-center gap-1 rounded-xl bg-zinc-900 text-white dark:bg-white dark:text-zinc-900 px-3 py-1.5">
              <Download className="w-4 h-4" /> Resume
            </a>
          </nav>
        </div>
      </header>

      {/* Hero */}
      <section id="home" className="mx-auto max-w-6xl px-4 py-16 md:py-24">
        <div className="grid md:grid-cols-2 gap-8 items-center">
          <motion.div initial={{ opacity: 0, y: 20 }} animate={{ opacity: 1, y: 0 }} transition={{ duration: 0.6 }}>
            <h1 className="text-3xl md:text-5xl font-extrabold leading-tight">
              {PROFILE.title}
            </h1>
            <p className="mt-2 text-lg md:text-xl text-zinc-600 dark:text-zinc-300">
              {PROFILE.subtitle}
            </p>
            <p className="mt-4 text-sm text-zinc-600 dark:text-zinc-400">
              Based in {PROFILE.location}. I build polished, performant games with clear architecture and clean code.
            </p>
            <div className="mt-6 flex flex-wrap gap-3">
              <a href="#projects" className="inline-flex items-center gap-2 rounded-2xl bg-zinc-900 text-white dark:bg-white dark:text-zinc-900 px-4 py-2.5 text-sm font-semibold">
                View Projects <ChevronRight className="w-4 h-4" />
              </a>
              <a href={PROFILE.github} target="_blank" rel="noreferrer" className="inline-flex items-center gap-2 rounded-2xl ring-1 ring-zinc-300 dark:ring-zinc-700 px-4 py-2.5 text-sm font-semibold">
                <Github className="w-4 h-4" /> GitHub
              </a>
              <a href={PROFILE.linkedin} target="_blank" rel="noreferrer" className="inline-flex items-center gap-2 rounded-2xl ring-1 ring-zinc-300 dark:ring-zinc-700 px-4 py-2.5 text-sm font-semibold">
                <Linkedin className="w-4 h-4" /> LinkedIn
              </a>
              <a href={PROFILE.itch} target="_blank" rel="noreferrer" className="inline-flex items-center gap-2 rounded-2xl ring-1 ring-zinc-300 dark:ring-zinc-700 px-4 py-2.5 text-sm font-semibold">
                <Globe className="w-4 h-4" /> Itch.io
              </a>
            </div>
          </motion.div>

          <motion.div initial={{ opacity: 0, scale: 0.95 }} animate={{ opacity: 1, scale: 1 }} transition={{ duration: 0.6, delay: 0.1 }}>
            <div className="relative rounded-3xl overflow-hidden shadow-xl ring-1 ring-zinc-200 dark:ring-zinc-800">
              <img
                src="https://images.unsplash.com/photo-1553484771-047a44eee27b?q=80&w=1200&auto=format&fit=crop"
                alt="Hero"
                className="w-full h-full object-cover"
              />
            </div>
          </motion.div>
        </div>
      </section>

      {/* Controls */}
      <section className="mx-auto max-w-6xl px-4">
        <div className="rounded-2xl bg-white/70 dark:bg-zinc-900/60 backdrop-blur ring-1 ring-zinc-200/60 dark:ring-zinc-800 p-4 md:p-5 flex flex-col md:flex-row gap-3 md:items-center md:justify-between">
          <div className="flex items-center gap-2 flex-1">
            <Search className="w-5 h-5 text-zinc-500" />
            <input
              value={query}
              onChange={(e) => setQuery(e.target.value)}
              placeholder="Search projects, tech, features..."
              className="w-full bg-transparent focus:outline-none text-sm"
            />
          </div>
          <div className="flex flex-wrap items-center gap-2">
            <Filter className="w-4 h-4 text-zinc-500" />
            {TAGS.map((t) => (
              <button
                key={t}
                onClick={() => setActiveTag(t)}
                className={classNames(
                  "px-3 py-1.5 rounded-full text-xs font-medium ring-1",
                  activeTag === t
                    ? "bg-zinc-900 text-white dark:bg-white dark:text-zinc-900 ring-zinc-900 dark:ring-white"
                    : "bg-zinc-100/60 dark:bg-zinc-800/60 text-zinc-700 dark:text-zinc-200 ring-zinc-300/70 dark:ring-zinc-700/70 hover:bg-zinc-200/60 dark:hover:bg-zinc-700"
                )}
              >
                {t}
              </button>
            ))}
          </div>
        </div>
      </section>

      {/* Projects */}
      <section id="projects" className="mx-auto max-w-6xl px-4 py-10 md:py-14">
        <div className="flex items-end justify-between mb-6">
          <div>
            <h2 className="text-2xl md:text-3xl font-bold">Featured Projects</h2>
            <p className="text-sm text-zinc-600 dark:text-zinc-400 mt-1">
              A mix of Unity 2D/3D games and a C++ turn-based prototype.
            </p>
          </div>
        </div>

        {filtered.length === 0 ? (
          <p className="text-sm text-zinc-500">No projects match that search/filter. Try clearing it.</p>
        ) : (
          <div className="grid sm:grid-cols-2 lg:grid-cols-3 gap-5 md:gap-6">
            {filtered.map((p) => (
              <ProjectCard key={p.id} p={p} />
            ))}
          </div>
        )}
      </section>

      {/* About */}
      <section id="about" className="mx-auto max-w-6xl px-4 pb-10 md:pb-14">
        <div className="rounded-3xl bg-white/70 dark:bg-zinc-900/60 ring-1 ring-zinc-200/60 dark:ring-zinc-800 p-6 md:p-8">
          <h2 className="text-2xl md:text-3xl font-bold">About Me</h2>
          <p className="mt-3 text-sm md:text-base text-zinc-700 dark:text-zinc-300 leading-relaxed">
            I’m a Unity Game Developer with 2+ years of experience at Mobzway Technologies, building casino-style and casual games for mobile and desktop. I focus on clean architecture (ScriptableObjects, Singletons, Object Pooling), performance, and polished UX.
          </p>
          <ul className="mt-4 grid sm:grid-cols-2 gap-2 text-sm text-zinc-700 dark:text-zinc-200">
            <li>• Unity (2D & 3D), C#</li>
            <li>• OOP, Design Patterns</li>
            <li>• UI Implementation & Animations</li>
            <li>• API Integration, Multiplayer basics</li>
            <li>• Git / GitHub, Clean Code</li>
          </ul>
        </div>
      </section>

      {/* Contact */}
      <section id="contact" className="mx-auto max-w-6xl px-4 pb-16">
        <div className="rounded-3xl bg-white/70 dark:bg-zinc-900/60 ring-1 ring-zinc-200/60 dark:ring-zinc-800 p-6 md:p-8">
          <h2 className="text-2xl md:text-3xl font-bold">Contact</h2>
          <p className="mt-3 text-sm md:text-base text-zinc-700 dark:text-zinc-300">
            Open to full-time roles and collaborations. Feel free to reach out!
          </p>
          <div className="mt-5 flex flex-wrap gap-3">
            <a
              href={`mailto:${PROFILE.email}`}
              className="inline-flex items-center gap-2 rounded-2xl bg-zinc-900 text-white dark:bg-white dark:text-zinc-900 px-4 py-2.5 text-sm font-semibold"
            >
              <Mail className="w-4 h-4" /> {PROFILE.email}
            </a>
            <a
              href={PROFILE.github}
              target="_blank"
              rel="noreferrer"
              className="inline-flex items-center gap-2 rounded-2xl ring-1 ring-zinc-300 dark:ring-zinc-700 px-4 py-2.5 text-sm font-semibold"
            >
              <Github className="w-4 h-4" /> GitHub
            </a>
            <a
              href={PROFILE.linkedin}
              target="_blank"
              rel="noreferrer"
              className="inline-flex items-center gap-2 rounded-2xl ring-1 ring-zinc-300 dark:ring-zinc-700 px-4 py-2.5 text-sm font-semibold"
            >
              <Linkedin className="w-4 h-4" /> LinkedIn
            </a>
          </div>
        </div>
      </section>

      {/* Footer */}
      <footer className="py-8 text-center text-xs text-zinc-500">
        © {new Date().getFullYear()} {PROFILE.name} • Built with React & Tailwind
      </footer>
    </div>
  );
}
