<head>
    <style>
        body {
            color: white;
            font-family: 'Inter', sans-serif;
            margin: 0;
            overflow-x: hidden; 
            justify-content: center;
            align-items: center;
            text-align: center;
            background-color: #353142; 
        }

        .sticky-header {
            position: sticky;
            top: 0;
            z-index: 50; 
            background-color: rgba(220, 38, 38, 0.9); 
            backdrop-filter: blur(5px);
            transition: background-color 0.3s ease-in-out;
        }

        .animate-on-scroll {
            opacity: 0;
            transform: translateY(50px);
            transition: opacity 0.8s ease-out, transform 0.8s ease-out;
        }

        .animate-on-scroll.is-visible {
            opacity: 1;
            transform: translateY(0);
        }

        #hero-section {
            color: white;
            position: relative;
            overflow: hidden; 
            background-color: #353142; 
            transition: transform 0.1s linear; 
            padding-right: 20px;
            padding-left: 20px;
        }

        .hero-title {
            font-size: 50px;
            opacity: 0;
            transform: translateY(20px) scale(0.9);
            transition: opacity 1s ease-out, transform 1s ease-out;
        }
        .hero-title.is-visible {
            opacity: 1;
            transform: translateY(0) scale(1);
        }

        .character-illustration {
            opacity: 0;
            transform: scale(0.8);
            transition: opacity 1s ease-out 0.2s, transform 1s ease-out 0.2s; 
        }
        .illustration {
            opacity: 0;
            transform: scale(0.8);
            transition: opacity 1s ease-out 0.2s, transform 1s ease-out 0.2s;
        }

        .character-illustration.is-visible {
            opacity: 1;
            transform: scale(1);
        }

        .illustration.is-visible {
            opacity: 1;
            transform: scale(1);
        }

        .hero-paragraph {
            font-size: 25px;
            opacity: 0;
            transform: translateY(20px);
            transition: opacity 1s ease-out 0.4s, transform 1s ease-out 0.4s;
        }
        .hero-paragraph.is-visible {
            opacity: 1;
            transform: translateY(0);
        }

        .profile-image {
            width: 450px;
            height: 450px;
        }

        .other-image {
            width: 450px;
            height: 450px;
        }
    </style>
</head>
<body class="min-h-screen text-white relative">
    <main class="relative z-10">
        <section id="hero-section" class="min-h-[calc(100vh-120px)] flex flex-col justify-center items-center text-center p-4 md:p-8">
            <h1 class="hero-title animate-on-scroll mb-2">
                Marcus White
            </h1>

            <div class="character-illustration animate-on-scroll">
                <img
                    src="assets/marcus.png"
                    alt="Marcus White"
                    class="profile-image"
                />
            </div>

            <p class="hero-paragraph animate-on-scroll">
                The air in Hancock County, Georgia hung heavy thick with humdity as the sun beamed from the sky. For Marcus, it was more than just a hot day. It was the day after his high school graduation. It was a momments that shoved been filled with pure happiness 
            </p>
            <p class="hero-paragraph animate-on-scroll">
                He cluteched his diploma, his name centered effortlessly. 
            </p>
        </section>

        <section class="min-h-screen flex flex-col justify-center items-center p-4 md:p-8">
            <div class="max-w-4xl mx-auto text-center animate-on-scroll">
                <div class="illustration animate-on-scroll">
                    <img
                        src="assets/diploma.png"
                        alt="Marcus Diploma"
                        class="other-image"
                    />
                </div>
                <p class="hero-paragraph animate-on-scroll">
                    Textbooks still lay scattered around, silencing the doubting whispers that followed him. His grandmother, a woman who was unable to stand without pain due to a long life of hard labor, stood next to him, her weak smile filled with pride. 
                </p>
                <h2 class="text-5xl md:text-6xl font-white mb-6">~~~</h2>
                <p class="hero-paragraph animate-on-scroll">
                    Marcus was accepted into a local state school, a proud moment for his family. However, even as he packed his bags, he remembered the college fair in his junior year. Even with his good GPA, counselors pointed him towards trades and community college, while his white peers were encouraged towards Ivy League schools and top 25 institutions. 
                </p>
            </div>
        </section>

        <section class="min-h-screen flex flex-col justify-center items-center p-4 md:p-8">
            <div class="max-w-4xl mx-auto text-center animate-on-scroll">
                <h2 class="text-5xl md:text-6xl font-white mb-6">He remembered the shift in expectation when he asked a question versus his white counterparts.</h2>
                <h2 class="text-5xl md:text-6xl font-white mb-6">He remembered his lifelong friends beginning to distance themselves.</h2>
                <h2 class="text-5xl md:text-6xl font-white mb-6">He remembered it all.</h2>
                <h2 class="text-5xl md:text-6xl font-white mb-6">~~~</h2>
                <p class="hero-paragraph animate-on-scroll">
                    College was a blur of textbooks and part-time jobs. He saw the statistics on how Black students received around 7% less help paying tution than their white peers.
                </p>
                <p class="hero-paragraph animate-on-scroll">
                    Even with his good GPA, counselors pointed him towards trades and community college, while his white peers were encouraged towards Ivy League schools and top 25 institutions. 
                </p>
                <p class="hero-paragraph animate-on-scroll">
                    Marcus was accepted into a local state school, a proud moment for his family. However, even as he packed his bags, he remembered the college fair in his junior year. 
                </p>
                <p class="hero-paragraph animate-on-scroll">
                    Even with his good GPA, counselors pointed him towards trades and community college, while his white peers were encouraged towards Ivy League schools and top 25 institutions. 
                </p>
            </div>
        </section>

        <section class="min-h-screen flex flex-col justify-center items-center p-4 md:p-8">
            <div class="max-w-4xl mx-auto text-center animate-on-scroll">
                <h2 class="text-5xl md:text-6xl font-black mb-6">A Legacy Forged</h2>
                <p class="text-lg md:text-xl leading-relaxed">
                    The dream became reality, a nation united under one banner. The sacrifices were immense, the journey arduous, but the legacy left behind was one of peace and prosperity, echoing through the ages. This is the culmination of a deeply emotional saga.
                </p>
            </div>
        </section>
    </main>

    <div class="fixed top-0 right-0 h-full w-2 z-40">
        <div
            id="scroll-progress-bar"
            class="bg-white w-full transition-all duration-100 ease-out"
            style="height: 0%;"
        ></div>
    </div>

    <script>
        function handleImageError(imgElement) {
            imgElement.onerror = null; 
            imgElement.src = 'https://placehold.co/384x384/880000/FFFFFF?text=Error+Loading+Image';
        }

        function handleScroll() {
            const scrollHeight = document.documentElement.scrollHeight - window.innerHeight;
            const currentScroll = window.scrollY;
            const scrollProgress = Math.min(100, Math.max(0, (currentScroll / scrollHeight) * 100));

            const progressBar = document.getElementById('scroll-progress-bar');
            if (progressBar) {
                progressBar.style.height = `${scrollProgress}%`;
            }

            const heroSection = document.getElementById('hero-section');
            if (heroSection) {
                const heroRect = heroSection.getBoundingClientRect();
                const parallaxOffset = (heroRect.top / window.innerHeight) * 50;
                heroSection.style.transform = `translateY(${parallaxOffset}px)`;
            }
        }

        const observerCallback = (entries, observer) => {
            entries.forEach(entry => {
                if (entry.isIntersecting) {
                    entry.target.classList.add('is-visible');
                } else {
                }
            });
        };

        let observer;

        document.addEventListener('DOMContentLoaded', () => {
            observer = new IntersectionObserver(observerCallback, {
                root: null, 
                rootMargin: '0px',
                threshold: 0.1 
            });

            document.querySelectorAll('.animate-on-scroll').forEach(element => {
                observer.observe(element);
            });

            window.addEventListener('scroll', handleScroll);

            handleScroll(); 
        });
    </script>
</body>