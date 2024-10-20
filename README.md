<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Nysa Crypto Article Feed</title>
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@300;400;500;600;700&display=swap" rel="stylesheet">
    <style>
        :root {
            --primary-color: #6d28d9;
            --secondary-color: #10b981;
            --text-color: #1f2937;
            --text-secondary: #4b5563;
            --border-color: #e5e7eb;
            --background-color: #f3f4f6;
            --card-background: #ffffff;
        }

        * {
            box-sizing: border-box;
            margin: 0;
            padding: 0;
        }

        body {
            font-family: 'Inter', sans-serif;
            background-color: var(--background-color);
            color: var(--text-color);
            line-height: 1.6;
        }

        .container {
            max-width: 800px;
            margin: 20px auto;
            padding: 0 15px;
        }

        .article {
            background-color: var(--card-background);
            border-radius: 12px;
            box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
            margin-bottom: 24px;
            overflow: hidden;
            transition: transform 0.3s ease, box-shadow 0.3s ease;
        }

        .article:hover {
            transform: translateY(-5px);
            box-shadow: 0 8px 12px rgba(0, 0, 0, 0.15);
        }

        .article-header {
            display: flex;
            align-items: center;
            padding: 16px;
            border-bottom: 1px solid var(--border-color);
        }

        .article-avatar {
            width: 48px;
            height: 48px;
            border-radius: 50%;
            object-fit: cover;
        }

        .article-info {
            margin-left: 16px;
            flex-grow: 1;
        }

        .article-author {
            font-weight: 600;
            font-size: 16px;
        }

        .article-date {
            font-size: 14px;
            color: var(--text-secondary);
        }

        .article-image {
            width: 100%;
            max-height: 400px;
            object-fit: cover;
        }

        .article-content {
            padding: 20px;
        }

        .article-title {
            font-size: 22px;
            font-weight: 700;
            margin-bottom: 12px;
            color: var(--primary-color);
        }

        .article-excerpt {
            font-size: 16px;
            color: var(--text-secondary);
            margin-bottom: 16px;
        }

        .read-more {
            display: inline-block;
            background-color: var(--secondary-color);
            color: white;
            padding: 8px 16px;
            border-radius: 20px;
            text-decoration: none;
            font-weight: 500;
            transition: background-color 0.3s ease;
            cursor: pointer;
        }

        .read-more:hover {
            background-color: #0ea572;
        }

        .article-tags {
            display: flex;
            flex-wrap: wrap;
            margin-top: 12px;
        }

        .tag {
            background-color: #e2e8f0;
            color: var(--text-secondary);
            font-size: 12px;
            padding: 4px 8px;
            border-radius: 16px;
            margin-right: 8px;
            margin-bottom: 8px;
        }

        .article-stats {
            display: flex;
            justify-content: space-between;
            align-items: center;
            padding: 12px 20px;
            background-color: #f8fafc;
            border-top: 1px solid var(--border-color);
            font-size: 14px;
            color: var(--text-secondary);
        }

        .stat {
            display: flex;
            align-items: center;
        }

        .stat i {
            margin-right: 8px;
            font-size: 16px;
        }

        .modal {
            display: none;
            position: fixed;
            z-index: 1000;
            left: 0;
            top: 0;
            width: 100%;
            height: 100%;
            overflow: auto;
            background-color: rgba(0,0,0,0.4);
        }

        .modal-content {
            background-color: #fefefe;
            margin: 5% auto;
            padding: 20px;
            border: 1px solid #888;
            width: 80%;
            max-width: 800px;
            border-radius: 12px;
            box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
        }

        .close {
            color: #aaa;
            float: right;
            font-size: 28px;
            font-weight: bold;
            cursor: pointer;
        }

        .close:hover,
        .close:focus {
            color: #000;
            text-decoration: none;
        }

        .full-article {
            max-height: 70vh;
            overflow-y: auto;
            padding-right: 20px;
        }

        @media (max-width: 640px) {
            .container {
                padding: 0 10px;
            }

            .article-header {
                padding: 12px;
            }

            .article-avatar {
                width: 40px;
                height: 40px;
            }

            .article-author {
                font-size: 14px;
            }

            .article-date {
                font-size: 12px;
            }

            .article-content {
                padding: 16px;
            }

            .article-title {
                font-size: 20px;
            }

            .article-excerpt {
                font-size: 14px;
            }

            .read-more {
                font-size: 14px;
                padding: 6px 12px;
            }

            .modal-content {
                width: 95%;
                margin: 10% auto;
            }

            .article-stats {
                flex-wrap: wrap;
            }

            .stat {
                margin-right: 12px;
                margin-bottom: 4px;
            }
        }
    </style>
</head>
<body>
    <div class="container" id="article-container"></div>

    <div id="articleModal" class="modal">
        <div class="modal-content">
            <span class="close">&times;</span>
            <div id="fullArticle" class="full-article"></div>
        </div>
    </div>

    <script>
        const articles = [
            {
                id: 1,
                author: "Nysa Crypto",
                avatar: "https://cryptoexchangereviews.com/wp-content/uploads/2021/04/coinbase-icon2.png",
                date: "Oct 20, 2024 • 5 min read",
                image: "https://i.postimg.cc/c19T41qj/Greek-and-Black-Vivid-Bold-Blocks-Electronics-and-Appliances-Banner.png",
                title: "The Future of Decentralized Finance: Nysa's Perspective",
                excerpt: "Explore the transformative potential of DeFi and how Nysa is contributing to this financial revolution. We delve into the latest trends, challenges, and opportunities in the world of decentralized finance.",
                fullContent: "Lorem ipsum dolor sit amet, consectetur adipiscing elit. Sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur. Excepteur sint occaecat cupidatat non proident, sunt in culpa qui officia deserunt mollit anim id est laborum.",
                readTime: 5,
                tags: ["DeFi", "Blockchain", "Crypto"],
                location: "Web4,World"
            },
            {
                id: 2,
                author: "Crypto Insights",
                avatar: "https://cryptoexchangereviews.com/wp-content/uploads/2021/04/coinbase-icon2.png",
                date: "Oct 19, 2024 • 7 min read",
                image: "https://i.postimg.cc/C5L74DfM/AD.png",
                title: "Bitcoin's Surge: Analyzing the Latest Bull Run",
                excerpt: "Bitcoin has reached new heights, breaking previous records. Our experts analyze the factors driving this surge and what it means for the future of cryptocurrency markets.",
                fullContent: "Lorem ipsum dolor sit amet, consectetur adipiscing elit. Sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur. Excepteur sint occaecat cupidatat non proident, sunt in culpa qui officia deserunt mollit anim id est laborum.",
                readTime: 7,
                tags: ["Bitcoin", "Market Analysis", "Cryptocurrency"],
                location: "Web3"
            },
            {
                id: 3,
                author: "Blockchain Weekly",
                avatar: "https://cryptoexchangereviews.com/wp-content/uploads/2021/04/coinbase-icon2.png",
                date: "Oct 18, 2024 • 6 min read",
                image: "https://i.postimg.cc/6q3gYT7K/Black-and-White-Typographic-and-Modern-Phone-Brand-Facebook-Ad.png",
                title: "The Rise of NFTs in the Art World",
                excerpt: "Non-fungible tokens are revolutionizing the art market. Discover how artists and collectors are embracing this new technology and what it means for the future of digital ownership.",
                fullContent: "Lorem ipsum dolor sit amet, consectetur adipiscing elit. Sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur. Excepteur sint occaecat cupidatat non proident, sunt in culpa qui officia deserunt mollit anim id est laborum.",
                readTime: 6,
                tags: ["NFT", "Digital Art", "Blockchain"],
                location: "Virtual Reality"
            }
        ];

        function createArticleElement(article) {
            const articleElement = document.createElement('article');
            articleElement.className = 'article';
            articleElement.innerHTML = `
                <div class="article-header">
                    <img src="${article.avatar}" alt="${article.author}" class="article-avatar">
                    <div class="article-info">
                        <div class="article-author">${article.author}</div>
                        <div class="article-date">${article.date}</div>
                    </div>
                </div>
                <img src="${article.image}" alt="${article.title}" class="article-image">
                <div class="article-content">
                    <h2 class="article-title">${article.title}</h2>
                    <p class="article-excerpt">${article.excerpt}</p>
                    <a class="read-more" data-id="${article.id}">Read More</a>
                    <div class="article-tags">
                        ${article.tags.map(tag => `<span class="tag">${tag}</span>`).join('')}
                    </div>
                </div>
                <div class="article-stats">
                    <span class="stat"><i class="fas fa-map-marker-alt"></i> ${article.location}</span>
                    <span class="stat"><i class="fas fa-clock"></i> ${article.readTime} min read</span>
                </div>
            `;

            return articleElement;
        }

        function renderArticles() {
            const container = document.getElementById('article-container');
            articles.forEach(article => {
                const articleElement = createArticleElement(article);
                container.appendChild(articleElement);
            });
        }

        document.addEventListener('DOMContentLoaded', () => {
            renderArticles();

            const modal = document.getElementById('articleModal');
            const fullArticle = document.getElementById('fullArticle');
            const closeBtn = document.getElementsByClassName('close')[0];

            document.addEventListener('click', (e) => {
                if (e.target.classList.contains('read-more')) {
                    const articleId = e.target.getAttribute('data-id');
                    const article = articles.find(a => a.id == articleId);
                    fullArticle.innerHTML = `
                        <h2>${article.title}</h2>
                        <p><i class="fas fa-map-marker-alt"></i> ${article.location}</p>
                        <p>${article.fullContent}</p>
                    `;
                    modal.style.display = 'block';
                }
            });

            closeBtn.onclick = () => {
                modal.style.display = 'none';
            };

            window.onclick = (e) => {
                if (e.target === modal) {
                    modal.style.display = 'none';
                }
            };
        });
    </script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/js/all.min.js"></script>
</body>
