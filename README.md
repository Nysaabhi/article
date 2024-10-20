
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
            margin-right: 4px;
        }

        @media (max-width: 640px) {
            .container {
                padding: 0 10px;
            }

            .header h1 {
                font-size: 24px;
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
        }
    </style>
</head>
<body>
    <div class="container" id="article-container"></div>

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
                views: 15000,
                readTime: 5,
                tags: ["DeFi", "Blockchain", "Crypto"]
            },
            {
                id: 2,
                author: "Crypto Insights",
                avatar: "https://cryptoexchangereviews.com/wp-content/uploads/2021/04/coinbase-icon2.png",
                date: "Oct 19, 2024 • 7 min read",
                image: "https://i.postimg.cc/C5L74DfM/AD.png",
                title: "Bitcoin's Surge: Analyzing the Latest Bull Run",
                excerpt: "Bitcoin has reached new heights, breaking previous records. Our experts analyze the factors driving this surge and what it means for the future of cryptocurrency markets.",
                views: 22000,
                readTime: 7,
                tags: ["Bitcoin", "Market Analysis", "Cryptocurrency"]
            },
            {
                id: 3,
                author: "Blockchain Weekly",
                avatar: "https://cryptoexchangereviews.com/wp-content/uploads/2021/04/coinbase-icon2.png",
                date: "Oct 18, 2024 • 6 min read",
                image: "https://i.postimg.cc/6q3gYT7K/Black-and-White-Typographic-and-Modern-Phone-Brand-Facebook-Ad.png",
                title: "The Rise of NFTs in the Art World",
                excerpt: "Non-fungible tokens are revolutionizing the art market. Discover how artists and collectors are embracing this new technology and what it means for the future of digital ownership.",
                views: 18500,
                readTime: 6,
                tags: ["NFT", "Digital Art", "Blockchain"]
            }
        ];

        function formatNumber(num) {
            if (num >= 1000000) return `${(num / 1000000).toFixed(1)}M`;
            if (num >= 1000) return `${(num / 1000).toFixed(1)}K`;
            return num.toString();
        }

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
                    <a href="#" class="read-more">Read More</a>
                    <div class="article-tags">
                        ${article.tags.map(tag => `<span class="tag">${tag}</span>`).join('')}
                    </div>
                </div>
                <div class="article-stats">
                    <span class="stat"><i class="fas fa-eye"></i> ${formatNumber(article.views)} views</span>
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

        document.addEventListener('DOMContentLoaded', renderArticles);
    </script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/js/all.min.js"></script>
</body>
