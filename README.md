import React, { useState } from 'react';
import { 
  Terminal, 
  ExternalLink, 
  Github, 
  Folder, 
  Cpu, 
  ShieldCheck, 
  CreditCard, 
  MapPin, 
  Gamepad2, 
  UserCheck, 
  Search,
  Sparkles
} from 'lucide-react';

const featuredProjects = [
  {
    id: "personal-portfolio",
    title: "Personal Portfolio",
    repoName: "PersonalPortifilio",
    url: "https://github.com/krishty21/PersonalPortifilio",
    category: "SYS / FRONTEND",
    badge: "v2.0-release",
    icon: <UserCheck className="w-5 h-5 text-cyan-400" />,
    description: "Modern, high-performance developer portfolio built with custom UI components, desktop-class window management, and terminal shell aesthetics.",
    techStack: ["React", "Three.js", "TailwindCSS", "Vite", "WebAudio"],
    stars: 6,
    command: "cat ./PersonalPortifilio/README.md"
  },
  {
    id: "void-pay",
    title: "VoidPay",
    repoName: "VoidPay",
    url: "https://github.com/krishty21/VoidPay",
    category: "FINTECH / SECURE",
    badge: "active-build",
    icon: <CreditCard className="w-5 h-5 text-emerald-400" />,
    description: "Encrypted digital payment and transaction handling system with secure key management, automated payload routing, and API gateway integrations.",
    techStack: ["Node.js", "Express", "PostgreSQL", "JWT", "Cryptography"],
    stars: 4,
    command: "node ./VoidPay/server.js --secure"
  },
  {
    id: "safe-route",
    title: "SafeRoute Navigation",
    repoName: "SafeRouteProject",
    url: "https://github.com/krishty21/SafeRouteProject",
    category: "GEO / SAFETY",
    badge: "featured-13★",
    icon: <MapPin className="w-5 h-5 text-amber-400" />,
    description: "Intelligent navigation and pathfinding tool designed to calculate routes using safety metrics, risk-factor weighting, and real-time mapping inputs.",
    techStack: ["Python", "FastAPI", "React", "Mapbox", "Geospatial Analysis"],
    stars: 13,
    command: "python3 ./SafeRoute/main.py --calc-route"
  },
  {
    id: "secure-chat",
    title: "SecureChat Engine",
    repoName: "SecureChat-Project",
    url: "https://github.com/krishty21/SecureChat-Project",
    category: "NETWORKING / E2EE",
    badge: "production",
    icon: <ShieldCheck className="w-5 h-5 text-purple-400" />,
    description: "End-to-end encrypted messaging application utilizing WebSockets for real-time streaming, AES-256 session encryption, and secure user sessions.",
    techStack: ["React", "Node.js", "WebSockets", "Socket.io", "Redis"],
    stars: 8,
    command: "./SecureChat/bin/chat-daemon --e2ee"
  },
  {
    id: "mines-game-ai",
    title: "Minesweeper DQN AI",
    repoName: "MinesGame",
    url: "https://github.com/krishty21/MinesGame",
    category: "AI / REINFORCEMENT",
    badge: "ml-model",
    icon: <Gamepad2 className="w-5 h-5 text-rose-400" />,
    description: "Custom Minesweeper game engine powered by a Deep Q-Network (DQN) reinforcement learning agent for automated grid analysis and strategic move predictions.",
    techStack: ["Python", "PyTorch", "NumPy", "Pygame", "Reinforcement Learning"],
    stars: 5,
    command: "python3 ./MinesGame/dqn_agent.py --train"
  }
];

export default function FeaturedProjectsShell() {
  const [activeTab, setActiveTab] = useState('all');
  const [searchQuery, setSearchQuery] = useState('');
  const [selectedProject, setSelectedProject] = useState(featuredProjects[0]);

  const filteredProjects = featuredProjects.filter(project => {
    const matchesSearch = project.title.toLowerCase().includes(searchQuery.toLowerCase()) ||
                          project.description.toLowerCase().includes(searchQuery.toLowerCase()) ||
                          project.techStack.some(t => t.toLowerCase().includes(searchQuery.toLowerCase()));
    return matchesSearch;
  });

  return (
    <section className="w-full max-w-6xl mx-auto py-12 px-4 font-mono">
      {/* Outer Shell Terminal Window */}
      <div className="bg-[#0d1117] border border-[#30363d] rounded-xl shadow-2xl overflow-hidden text-[#c9d1d9]">
        
        {/* Terminal Top Window Control Bar */}
        <div className="bg-[#161b22] px-4 py-3 border-b border-[#30363d] flex items-center justify-between select-none">
          <div className="flex items-center space-x-2">
            <div className="w-3 h-3 rounded-full bg-[#ff5f56] border border-[#e0443e] cursor-pointer hover:opacity-80 transition-opacity"></div>
            <div className="w-3 h-3 rounded-full bg-[#ffbd2e] border border-[#aea12b] cursor-pointer hover:opacity-80 transition-opacity"></div>
            <div className="w-3 h-3 rounded-full bg-[#27c93f] border border-[#1bac2c] cursor-pointer hover:opacity-80 transition-opacity"></div>
            <span className="text-xs text-[#8b949e] ml-2 font-mono flex items-center gap-1">
              <Terminal className="w-3.5 h-3.5" />
              dhruvith@hyprland: ~/projects
            </span>
          </div>

          {/* Shell Status Indicators */}
          <div className="hidden sm:flex items-center space-x-3 text-xs text-[#8b949e]">
            <span className="px-2 py-0.5 rounded bg-[#21262d] border border-[#30363d] text-emerald-400">
              ● zsh 5.9
            </span>
            <span className="px-2 py-0.5 rounded bg-[#21262d] border border-[#30363d] text-cyan-400">
              UTF-8
            </span>
          </div>
        </div>

        {/* Terminal Sub-Header Prompt Line */}
        <div className="p-4 bg-[#0d1117]/80 border-b border-[#21262d] text-sm">
          <div className="flex flex-wrap items-center gap-2 text-[#8b949e]">
            <span className="text-emerald-400 font-bold">krishty21@hyprland</span>
            <span>:</span>
            <span className="text-cyan-400 font-bold">~/featured-projects</span>
            <span className="text-purple-400 font-bold">(main)</span>
            <span>$</span>
            <span className="text-[#e6edf3]">./fetch_repositories.sh --list-featured</span>
          </div>
          
          {/* Filter / Interactive Search Prompt Bar */}
          <div className="mt-3 flex flex-col sm:flex-row items-stretch sm:items-center justify-between gap-3 bg-[#161b22] p-2.5 rounded-lg border border-[#30363d]">
            <div className="flex items-center gap-2 text-xs text-[#8b949e] pl-1">
              <Sparkles className="w-4 h-4 text-amber-400 shrink-0" />
              <span>Loaded <strong className="text-[#e6edf3]">{featuredProjects.length}</strong> core repositories</span>
            </div>

            <div className="relative flex-1 max-w-xs">
              <Search className="w-3.5 h-3.5 absolute left-2.5 top-1/2 -translate-y-1/2 text-[#8b949e]" />
              <input
                type="text"
                placeholder="grep project or tech stack..."
                value={searchQuery}
                onChange={(e) => setSearchQuery(e.target.value)}
                className="w-full bg-[#0d1117] text-xs text-[#e6edf3] pl-8 pr-3 py-1.5 rounded border border-[#30363d] focus:outline-none focus:border-cyan-500 transition-colors placeholder-[#484f58]"
              />
            </div>
          </div>
        </div>

        {/* Projects Grid Section inside Shell Body */}
        <div className="p-6 grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-5 bg-[#0d1117]">
          {filteredProjects.map((project) => (
            <div 
              key={project.id}
              onClick={() => setSelectedProject(project)}
              className={`group relative bg-[#161b22] border rounded-lg p-5 transition-all duration-200 cursor-pointer flex flex-col justify-between hover:-translate-y-0.5 ${
                selectedProject.id === project.id 
                  ? 'border-cyan-500 shadow-[0_0_15px_rgba(6,182,212,0.15)] bg-[#1c2129]' 
                  : 'border-[#30363d] hover:border-[#8b949e]'
              }`}
            >
              {/* Card Header */}
              <div>
                <div className="flex items-center justify-between mb-3">
                  <div className="flex items-center gap-2">
                    <div className="p-2 rounded bg-[#21262d] border border-[#30363d]">
                      {project.icon}
                    </div>
                    <div>
                      <span className="text-[10px] tracking-wider text-[#8b949e] font-semibold block uppercase">
                        {project.category}
                      </span>
                      <h3 className="text-base font-bold text-[#e6edf3] group-hover:text-cyan-400 transition-colors">
                        {project.title}
                      </h3>
                    </div>
                  </div>
                  <span className="text-[10px] px-2 py-0.5 rounded bg-[#21262d] text-cyan-300 border border-cyan-500/20 font-mono">
                    {project.badge}
                  </span>
                </div>

                {/* Simulated Terminal Command Box */}
                <div className="bg-[#0d1117] p-2 rounded text-[11px] text-[#8b949e] font-mono mb-3 border border-[#21262d] flex items-center justify-between">
                  <span className="truncate text-emerald-400/90">{project.command}</span>
                  <Folder className="w-3.5 h-3.5 text-[#484f58] shrink-0 ml-1" />
                </div>

                {/* Project Description */}
                <p className="text-xs text-[#8b949e] leading-relaxed mb-4">
                  {project.description}
                </p>
              </div>

              {/* Card Footer: Tech Stack Tags & External Links */}
              <div>
                <div className="flex flex-wrap gap-1.5 mb-4">
                  {project.techStack.map((tech, idx) => (
                    <span 
                      key={idx}
                      className="text-[10px] px-2 py-0.5 rounded bg-[#21262d] text-[#c9d1d9] border border-[#30363d]"
                    >
                      {tech}
                    </span>
                  ))}
                </div>

                <div className="flex items-center justify-between pt-3 border-t border-[#21262d] text-xs">
                  <span className="text-[#8b949e] text-[11px]">
                    Repo: <strong className="text-[#e6edf3] font-normal">{project.repoName}</strong>
                  </span>
                  
                  <a
                    href={project.url}
                    target="_blank"
                    rel="noopener noreferrer"
                    onClick={(e) => e.stopPropagation()}
                    className="inline-flex items-center gap-1 text-xs text-cyan-400 hover:text-cyan-300 hover:underline font-semibold"
                  >
                    <Github className="w-3.5 h-3.5" />
                    <span>Source</span>
                    <ExternalLink className="w-3 h-3 ml-0.5" />
                  </a>
                </div>
              </div>
            </div>
          ))}
        </div>

        {/* Shell Footer / Interactive Drawer Details */}
        <div className="bg-[#161b22] px-6 py-4 border-t border-[#30363d] flex flex-col sm:flex-row items-center justify-between text-xs text-[#8b949e] gap-3">
          <div className="flex items-center gap-2">
            <span className="inline-block w-2 h-2 rounded-full bg-emerald-400 animate-pulse"></span>
            <span>Selected target: <strong className="text-cyan-400">{selectedProject.repoName}</strong></span>
          </div>

          <div className="flex items-center gap-4">
            <a 
              href={selectedProject.url} 
              target="_blank" 
              rel="noopener noreferrer"
              className="px-3 py-1.5 rounded bg-cyan-500/10 text-cyan-400 border border-cyan-500/30 hover:bg-cyan-500/20 transition-all font-semibold flex items-center gap-1.5"
            >
              <Github className="w-3.5 h-3.5" />
              <span>Clone Repository</span>
            </a>
          </div>
        </div>

      </div>
    </section>
  );
}
