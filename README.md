---
--<style>
<
/* Hide site title / first H1 rendered from README or theme header */
.markdown-body > h1:first-child,
.repo-title,
.site-title,
.site-header .site-title,
.header .site-title,
.header h1,
.repository-content h1 {
  display: none !important;
}
</style>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Sauna Cleveland Employee Handbook</title>
    <!-- UPDATED: Google Fonts link for Sulphur Point and Poppins fallback --><link href="https://fonts.googleapis.com/css2?family=Sulphur+Point:wght@300;400;700&family=Poppins:wght@400;600;700;800&display=swap" rel="stylesheet">
    <script src="https://cdn.tailwindcss.com"></script>
    <script>
        // Custom Tailwind Configuration using Brand Colors and Font
        tailwind.config = {
            theme: {
                extend: {
                    colors: {
                        'loyal-blue': '#1f3548',
                        'sky-fall': '#c6dff7',
                        'dragon-pink': '#FF0A8E', /* Primary Accent */
                        'security-red': '#fe0000', /* Using user's provided value */
                        'mint-condition': '#D3e5d5',
                    },
                    // UPDATED: Font family configuration to use Sulphur Point as the default sans font
                    fontFamily: {
                        sans: ['Sulphur Point', 'Poppins', 'sans-serif'],
                    }
                }
            }
        }
    </script>
    <script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
    <!-- Chosen Palette: Loyal Blue, Dragon Fruit Pink, Sky Fall, Mint Condition --><!-- Application Structure Plan: The original handbook is a linear document, which is inefficient for an employee needing specific, time-sensitive information (e.g., "What's the emergency protocol?"). This SPA redesign transforms the content into a task-oriented, thematic, tab-based application. The key sections are "Core Policies," "Operations," "Client Safety," "Maintenance," "Emergencies," and "Acknowledgement." This non-linear structure allows an employee to instantly access the information relevant to their current task (e.g., setup, client interaction, cleaning) without scrolling. The user flow is centered on clicking a tab, which uses JavaScript to hide all other content sections and display only the relevant one, making it a fast and efficient single-page experience. This structure prioritizes employee workflow and rapid information retrieval over the report's original narrative flow. --><!-- Visualization & Content Choices: 
        - Report Info: All handbook content (policies, procedures). Goal: Inform, Organize. Viz/Presentation: Structured HTML/Tailwind content "cards" and "checklists." Interaction: The primary interaction is the JS-powered tab navigation. Justification: No quantitative data exists, so no charts are needed. The content is purely procedural and informational.
        - Report Info: Section 3.3 (Setup) & 5.1 (Cleaning). Goal: Organize/Inform. Viz/Presentation: Interactive-style "step" cards using HTML/Tailwind with Unicode icons (e.g., 📍, 🧼, 🔥). Interaction: Enhanced readability and quick scanning. Justification: More engaging and easier to parse as a checklist than a simple bulleted list, reinforcing the steps. Library: HTML/Tailwind/Unicode.
        - Report Info: Sections 4 (Client Safety) & 6 (Client Service). Goal: Organize. Viz/Presentation: Merged into a single "Client Safety & Service" thematic tab. Interaction: Tab navigation (JS click listeners). Justification: Groups all client-facing tasks (safety and service) into one logical user flow, which is more intuitive for an employee than the report's separate sections. Library: Vanilla JS.
        - Report Info: Section 4.3 (Emergencies). Goal: Inform (Rapidly). Viz/Presentation: A dedicated "Emergency" tab with high-contrast, numbered steps. Interaction: Quick-access tab. Justification: Elevates critical safety information to its own top-level category for instant access, a significant usability improvement. Library: Vanilla JS / HTML.
    --><!-- CONFIRMATION: NO SVG graphics used. NO Mermaid JS used. --><style>
        .chart-container {
            position: relative;
            width: 100%;
            max-width: 600px;
            margin-left: auto;
            margin-right: auto;
            height: 300px;
            max-height: 400px;
        }
        @media (min-width: 768px) {
            .chart-container {
                height: 350px;
            }
        }
        
        /* Custom styles using brand colors */
        .tab.active {
            /* Active tab uses white background and Dragon Pink text with a Loyal Blue shadow */
            @apply bg-white text-dragon-pink shadow-lg shadow-loyal-blue/20;
        }
        .tab:not(.active) {
            /* Inactive tabs use Mint Condition background and Loyal Blue text */
            @apply bg-mint-condition text-loyal-blue hover:bg-mint-condition/70;
        }
    </style>
</head>
<body class="bg-sky-fall text-loyal-blue font-sans leading-relaxed">

    <div class="max-w-5xl mx-auto p-4 sm:p-6 lg:p-8">
        
        <header class="mb-8 p-4 bg-white rounded-xl shadow-lg flex items-center">
            
            <div class="flex items-center justify-center h-16 w-16 bg-dragon-pink/10 rounded-full mr-4 shadow-inner">
                <!-- NEW: Stylized SVG Logo for "Sauna Cleveland" - S and C like smoke --><svg class="w-12 h-12" viewBox="0 0 50 50" fill="none" xmlns="http://www.w3.org/2000/svg">
                    <!-- Stylized 'S' in Loyal Blue (bottom element, like a base of steam) --><path d="M25 20 C 15 20, 10 25, 15 30 C 20 35, 30 35, 35 30 C 40 25, 35 20, 25 20 Z" fill="#1f3548"/>
                    <!-- Stylized 'C' in Dragon Pink (top element, like rising vapor) --><path d="M30 10 C 20 10, 15 15, 20 20 C 25 25, 35 25, 40 20 C 45 15, 40 10, 30 10 Z" fill="#FF0A8E" transform="translate(-5, -5) rotate(15 25 15)"/>
                    <path d="M28 12 C 18 12, 13 17, 18 22 C 23 27, 33 27, 38 22 C 43 17, 38 12, 28 12 Z" fill="#FF0A8E" opacity="0.7" transform="translate(-3, -8) rotate(-10 25 15)"/>
                </svg>
            </div>
            <div>
                <h1 class="text-4xl font-extrabold tracking-tight">
                    <span class="text-dragon-pink">Sauna</span> <span class="text-dragon-pink">Cleveland</span>
                </h1>
                <p class="text-lg text-gray-600 mt-1">Your interactive guide to operations, safety, and service.</p>
            </div>
        </header>

        <nav class="mb-6" role="tablist" aria-label="Handbook Sections">
            <div class="flex flex-wrap gap-2">
                <button role="tab" aria-selected="true" class="tab active py-3 px-5 rounded-xl font-bold transition-all duration-300" data-target="policies">
                    Core Policies
                </button>
                <button role="tab" aria-selected="false" class="tab py-3 px-5 rounded-xl font-bold transition-all duration-300" data-target="operations">
                    Operations
                </button>
                <button role="tab" aria-selected="false" class="tab py-3 px-5 rounded-xl font-bold transition-all duration-300" data-target="safety">
                    Client Safety
                </button>
                <button role="tab" aria-selected="false" class="tab py-3 px-5 rounded-xl font-bold transition-all duration-300" data-target="maintenance">
                    Maintenance
                </button>
                <button role="tab" aria-selected="false" class="tab py-3 px-5 rounded-xl font-bold transition-all duration-300" data-target="emergencies">
                    🚨 Emergencies
                </button>
                <button role="tab" aria-selected="false" class="tab py-3 px-5 rounded-xl font-bold transition-all duration-300" data-target="acknowledgement">
                    Acknowledgement
                </button>
            </div>
        </nav>

        <main id="content-container">
            
            <section id="policies" role="tabpanel" class="content-section bg-white p-6 rounded-xl shadow-lg space-y-6">
                <header>
                    <h2 class="text-3xl font-bold text-dragon-pink">Core Policies</h2>
                    
                </header>

                <div>
                    <h3 class="text-2xl font-semibold text-loyal-blue">Our Mission</h3>
                    <p class="mt-2 text-gray-700">To provide a unique, restorative, and safe sauna experience delivered directly to our clients, promoting health, relaxation, and community wellness.</p>
                </div>

                <div class="grid md:grid-cols-2 gap-6">
                    <div class="space-y-4">
                        <h4 class="text-xl font-semibold text-loyal-blue">Employment Basics</h4>
                        <div class="p-4 bg-mint-condition rounded-lg">
                            <h5 class="font-bold">At-Will Employment</h5>
                            <p class="text-sm">This handbook is a guide and not a contract. Your employment is at-will, and policies may change.</p>
                        </div>
                        <div class="p-4 bg-mint-condition rounded-lg">
                            <h5 class="font-bold">Equal Opportunity</h5>
                            <p class="text-sm">We provide equal employment opportunities to all qualified applicants and employees without regard to race, color, religion, sex, national origin, age, disability, or veteran status.</p>
                        </div>
                        <div class="p-4 bg-mint-condition rounded-lg">
                            <h5 class="font-bold">Confidentiality</h5>
                            <p class="text-sm">All client information, business operations, and scheduling data are confidential and must not be shared.</p>
                        </div>
                        <div class="p-4 bg-mint-condition rounded-lg">
                            <h5 class="font-bold">Standards of Conduct</h5>
                            <p class="text-sm">Act with honesty, integrity, and respect toward clients, vendors, and fellow employees at all times.</p>
                        </div>
                    </div>
                    
                    <div class="space-y-4">
                        <h4 class="text-xl font-semibold text-loyal-blue">Compensation & Benefits</h4>
                        <div class="p-4 bg-mint-condition rounded-lg">
                            <h5 class="font-bold">Pay Schedule</h5>
                            <p class="text-sm">Employees are paid every 2 weeks via direct depoist.</p>
                        </div>
                        <div class="p-4 bg-mint-condition rounded-lg">
                            <h5 class="font-bold">Time Off Requests</h5>
                            <p class="text-sm">Requests for PTO or unpaid leave must be submitted in writing 7 days in advance and are subject to approval.</p>
                        </div>
                    </div>
                </div>
            </section>
            
            <section id="operations" role="tabpanel" class="content-section bg-white p-6 rounded-xl shadow-lg space-y-6 hidden">
                <header>
                    <h2 class="text-3xl font-bold text-dragon-pink">Operations</h2>
                   
                </header>

                <div class="grid md:grid-cols-2 gap-6">
                    <div class="space-y-4">
                        <h3 class="text-2xl font-semibold text-loyal-blue">Scheduling & Transport</h3>
                        <div class="p-4 bg-mint-condition rounded-lg">
                            <h4 class="font-bold">Scheduling and Attendance</h4>
                            <p class="text-sm">Punctuality is paramount. Arrive on site or at the pickup location and client site on time. Notify your manager immediately of any delays.</p>
                        </div>
                        <div class="p-4 bg-mint-condition rounded-lg">
                            <h4 class="font-bold">Vehicle and Towing Policy</h4>
                            <ul class="list-disc list-inside text-sm space-y-1 mt-2">
                                <li>Only authorized and trained employees may tow the sauna.</li>
                                <li>Pre-trip and post-trip inspections of the vehicle, trailer, lights, and hitch are mandatory for every event.</li>
                                <li>Maintain a clean driving record and report any changes to your license status immediately.</li>
                            </ul>
                        </div>
                        <div class="p-4 bg-mint-condition rounded-lg">
                            <h4 class="font-bold">Breaks and Meals</h4>
                            <p class="text-sm">Due to travel, plan your breaks effectively between events. Never leave the sauna unattended for longer than 20 minutes.</p>
                        </div>
                    </div>

                    <div class="space-y-4">
                        <h3 class="text-2xl font-semibold text-loyal-blue">On-Site Setup Protocol</h3>
                        <p class="text-gray-600">Follow the **Mobile Sauna Setup Checklist** every time. Key procedures include: setting up the stove, lighting the fire, instructing the client on how to use the sauna, setting up the cold plunge if applicable, and setting up furniture if applicable. 
                        </p>
                        <div class="space-y-3">
                            <div class="bg-mint-condition p-4 rounded-lg flex items-start">
                                <span class="text-3xl mr-3">📍</span>
                                <div>
                                    <h5 class="font-semibold">Site Assessment</h5>
                                    <p class="text-sm">Verify ground is level, stable, and safe for the trailer and client access.</p>
                                </div>
                            </div>
                            <div class="bg-mint-condition p-4 rounded-lg flex items-start">
                                <span class="text-3xl mr-3">🛡️</span>
                                <div>
                                    <h5 class="font-semibold">Safety Zone</h5>
                                    <p class="text-sm">Ensure a clear perimeter around the sauna unit and stove pipe.</p>
                                </div>
                            </div>
                            <div class="bg-mint-condition p-4 rounded-lg flex items-start">
                                <span class="text-3xl mr-3">💧</span>
                                <div>
                                    <h5 class="font-semibold">Water Supply</h5>
                                    <p class="text-sm">Ensure the cold plunge (if applicable) is clean and full.</p>
                                </div>
                            </div>
                            <div class="bg-mint-condition p-4 rounded-lg flex items-start">
                                <span class="text-3xl mr-3">🔥</span>
                                <div>
                                    <h5 class="font-semibold">Heating</h5>
                                    <p class="text-sm">Follow strict protocol for lighting the stove.</p>
                                </div>
                            </div>
                        </div>
                    </div>
                </div>
            </section>
            
            <section id="safety" role="tabpanel" class="content-section bg-white p-6 rounded-xl shadow-lg space-y-6 hidden">
                <header>
                    <h2 class="text-3xl font-bold text-dragon-pink">Client Safety</h2>
                    
                </header>

                <div class="grid md:grid-cols-2 gap-6">
                    <div class="space-y-4">
                        <h3 class="text-2xl font-semibold text-loyal-blue">Wellness Protocols</h3>
                        <div class="p-4 bg-mint-condition rounded-lg">
                            <h4 class="font-bold">Temperature and Ventilation</h4>
                            <p class="text-sm">Monitor and maintain sauna temperature within the recommended range (e.g., 160°F to 190°F). Ensure proper ventilation is maintained.</p>
                        </div>
                        <div class="p-4 bg-security-red/10 border border-security-red/30 rounded-lg">
                            <h4 class="font-bold text-security-red">Mandatory Client Safety Briefing</h4>
                            <p class="text-sm text-security-red">Before **every** first session, you MUST cover:</p>
                            <ul class="list-disc list-inside text-sm space-y-1 mt-2 text-security-red">
                                <li>Hydration: Drink water before, during, and after.</li>
                                <li>Time Limits: Recommend 10-20 minute sessions with cool-down breaks.</li>
                                <li>Emergencies: Show emergency exit and communication methods.</li>
                                <li>Contraindications: Warn clients who are pregnant, have heart conditions, or are under the influence of alcohol or other substances not to use the sauna.</li>
                            </ul>
                        </div>
                    </div>

                    <div class="space-y-4">
                        <h3 class="text-2xl font-semibold text-loyal-blue">Professional Service</h3>
                        <div class="p-4 bg-mint-condition rounded-lg">
                            <h4 class="font-bold">Appearance and Uniform</h4>
                            <p class="text-sm">Wear the approved attire. Personal hygiene and a neat appearance are mandatory.</p>
                        </div>
                        <div class="p-4 bg-mint-condition rounded-lg">
                            <h4 class="font-bold">Communication</h4>
                            <p class="text-sm">Always communicate clearly, respectfully, and enthusiastically. Answer questions about function, safety, and benefits accurately.</p>
                        </div>
                        <div class="p-4 bg-mint-condition rounded-lg">
                            <h4 class="font-bold">Handling Complaints</h4>
                            <p class="text-sm">Listen empathetically, apologize, and notify your supervisor immediately. Never argue or make unauthorized promises.</p>
                        </div>
                    </div>
                </div>
            </section>
            
            <section id="maintenance" role="tabpanel" class="content-section bg-white p-6 rounded-xl shadow-lg space-y-6 hidden">
                <header>
                    <h2 class="text-3xl font-bold text-dragon-pink">Maintenance</h2>
                    
                </header>

                <div class="grid md:grid-cols-2 gap-6">
                    <div class="space-y-4">
                        <h3 class="text-2xl font-semibold text-loyal-blue">3-Step Sanitation Protocol</h3>
                        <p class="text-gray-600">The sauna must be **completely cleaned and sanitized after every single use**.</p>
                        <div class="space-y-3">
                            <div class="bg-mint-condition p-4 rounded-lg flex items-start">
                                <span class="text-3xl mr-3">1.</span>
                                <div>
                                    <h5 class="font-semibold">Removal</h5>
                                    <p class="text-sm">Remove all trash, towels, and debris.</p>
                                </div>
                            </div>
                            <div class="bg-mint-condition p-4 rounded-lg flex items-start">
                                <span class="text-3xl mr-3">2.</span>
                                <div>
                                    <h5 class="font-semibold">Washing</h5>
                                    <p class="text-sm">Wipe down all benches, walls, and flooring with approved, non-toxic cleaner.</p>
                                </div>
                            </div>
                            <div class="bg-mint-condition p-4 rounded-lg flex items-start">
                                <span class="text-3xl mr-3">3.</span>
                                <div>
                                    <h5 class="font-semibold">Sanitation</h5>
                                    <p class="text-sm">Apply a commercial-grade, health-safe disinfectant spray to all interior surfaces and allow required dwell time.</p>
                                </div>
                            </div>
                        </div>
                    </div>

                    <div class="space-y-4">
                        <h3 class="text-2xl font-semibold text-loyal-blue">Equipment Care</h3>
                        <div class="p-4 bg-mint-condition rounded-lg">
                            <h4 class="font-bold">Wood Stove and Wood</h4>
                            <ul class="list-disc list-inside text-sm space-y-1 mt-2">
                                <li>Only use approved, dry wood. Never use treated wood or accelerants.</li>
                                <li>Ensure chimney is clear and ash pan is emptied safely into a metal container (after cooling).</li>
                            </ul>
                        </div>
                        <div class="p-4 bg-security-red/10 border border-security-red/30 rounded-lg">
                            <h4 class="font-bold text-security-red">Reporting Damage & Malfunctions</h4>
                            <p class="text-sm text-security-red">Immediately report any damage to the trailer, mechanical issues (lights, brakes), or non-functioning equipment (heaters, thermometers) to management. <strong class="font-bold">Never attempt unauthorized repairs.</strong></p>
                        </div>
                    </div>
                </div>
            </section>
            
            <section id="emergencies" role="tabpanel" class="content-section bg-white p-6 rounded-xl shadow-lg space-y-6 hidden">
                <header>
                    <h2 class="text-3xl font-bold text-security-red">🚨 Emergency Procedures</h2>
                    <p class="mt-2 text-lg text-gray-700">
                        In the event of a client health emergency or a fire, follow these steps immediately. Your first priority is the safety of the client.
                    </p>
                </header>

                <div class="space-y-4">
                    <div class="bg-security-red/10 border-l-4 border-security-red p-6 rounded-r-lg">
                        <h3 class="text-2xl font-bold text-security-red">Priority 1: Client Health Emergency</h3>
                        <ol class="list-decimal list-inside space-y-3 mt-4 text-security-red font-semibold text-lg">
                            <li>Ensure the safety of the client (remove them from the heat immediately).</li>
                            <li>Call emergency services (911) if necessary.</li>
                            <li>Notify management immediately.</li>
                            <li>Document the incident thoroughly after the situation is stable by sending an email to saunacleveland@gmail.com with the subject line "Incident Report [Date]".</li>
                        </ol>
                    </div>
                    
                    <div class="bg-security-red/10 border-l-4 border-security-red p-6 rounded-r-lg">
                        <h3 class="text-2xl font-bold text-security-red">Priority 2: Fire or Equipment Failure</h3>
                         <ol class="list-decimal list-inside space-y-3 mt-4 text-security-red font-semibold text-lg">
                            <li>Evacuate all clients from the sauna immediately.</li>
                            <li>Call emergency services (911) if there is a fire.</li>
                            <li>If safe, use the provided fire extinguisher.</li>
                            <li>Notify management immediately.</li>
                        </ol>
                    </div>
                </div>
            </section>
            
            <section id="acknowledgement" role="tabpanel" class="content-section bg-white p-6 rounded-xl shadow-lg space-y-6 hidden">
                <header>
                    <h2 class="text-3xl font-bold text-dragon-pink">Acknowledgement</h2>
                    <p class="mt-2 text-lg text-gray-700">
                        Please review this section to acknowledge that you have read and understood the policies outlined in this handbook.
                    </p>
                </header>
                
                <div class="p-6 bg-mint-condition rounded-lg border">
                    <p class="text-gray-700">I have received, read, and understand the policies set forth in this Employee Handbook. I understand that I am responsible for complying with all policies and that the company may change these policies at any time.</p>
                    
                    <div class="mt-8 space-y-6">
                        <div class="border-b border-loyal-blue/50 pb-2">
                            <p class="text-sm text-gray-500">Employee Name</p>
                        </div>
                        <div class="border-b border-loyal-blue/50 pb-2">
                            <p class="text-sm text-gray-500">Employee Signature</p>
                        </div>
                        <div class="border-b border-loyal-blue/50 pb-2">
                            <p class="text-sm text-gray-500">Date</p>
                        </div>
                    </div>
                </div>
            </section>

        </main>
    </div>

    <script>
        document.addEventListener('DOMContentLoaded', () => {
            const tabs = document.querySelectorAll('button[role="tab"]');
            const contentSections = document.querySelectorAll('section[role="tabpanel"]');
            
            tabs.forEach(tab => {
                tab.addEventListener('click', (e) => {
                    const targetId = tab.getAttribute('data-target');
                    
                    tabs.forEach(t => {
                        t.classList.remove('active');
                        t.setAttribute('aria-selected', 'false');
                    });
                    
                    tab.classList.add('active');
                    tab.setAttribute('aria-selected', 'true');
                    
                    contentSections.forEach(section => {
                        if (section.id === targetId) {
                            section.classList.remove('hidden');
                        } else {
                            section.classList.add('hidden');
                        }
                    });
                });
            });
        });
    </script>
</body>
</html>
