<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>موقع اذكار المسلم</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: 'Segoe UI', 'Arial', sans-serif;
            background: linear-gradient(135deg, #0F3460 0%, #16213E 25%, #1A472A 50%, #0F3460 75%, #533483 100%);
            background-attachment: fixed;
            background-size: 400% 400%;
            min-height: 100vh;
            color: #333;
            position: relative;
        }

        body::before {
            content: '';
            position: fixed;
            top: 0;
            left: 0;
            right: 0;
            bottom: 0;
            background-image: 
                radial-gradient(circle at 20% 30%, rgba(255, 215, 0, 0.05) 0%, transparent 50%),
                radial-gradient(circle at 80% 70%, rgba(220, 180, 105, 0.05) 0%, transparent 50%);
            pointer-events: none;
            z-index: 0;
        }

        .header {
            background: linear-gradient(135deg, #1A472A 0%, #0F3460 50%, #16213E 100%);
            color: white;
            padding: 2rem;
            text-align: center;
            box-shadow: 0 4px 6px rgba(0, 0, 0, 0.2);
            position: relative;
            border-bottom: 3px solid #FFD700;
        }

        .header::before {
            content: '✦';
            position: absolute;
            top: 10px;
            right: 20px;
            font-size: 1.5rem;
            color: #FFD700;
            opacity: 0.6;
        }

        .header::after {
            content: '✦';
            position: absolute;
            top: 10px;
            left: 20px;
            font-size: 1.5rem;
            color: #FFD700;
            opacity: 0.6;
        }

        .header h1 {
            font-size: 2.5rem;
            margin-bottom: 0.5rem;
            font-weight: 700;
        }

        .header p {
            font-size: 1.1rem;
            opacity: 0.9;
        }

        .container {
            max-width: 1200px;
            margin: 2rem auto;
            padding: 0 1rem;
        }

        .search-bar {
            text-align: center;
            margin-bottom: 2rem;
        }

        .search-bar input {
            width: 100%;
            max-width: 500px;
            padding: 0.75rem 1rem;
            border: 2px solid #FFD700;
            border-radius: 50px;
            font-size: 1rem;
            box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
            background: rgba(255, 255, 255, 0.95);
            color: #1A472A;
            transition: all 0.3s ease;
        }

        .search-bar input:focus {
            outline: none;
            box-shadow: 0 0 15px rgba(255, 215, 0, 0.3);
            background: white;
        }

        .search-bar input::placeholder {
            color: #999;
        }

        .categories {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
            gap: 1.5rem;
            margin-bottom: 2rem;
        }

        .category-btn {
            background: white;
            border: 2px solid #0F3460;
            padding: 1.5rem;
            border-radius: 10px;
            cursor: pointer;
            font-size: 1.1rem;
            font-weight: 600;
            color: #1A472A;
            box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
            transition: all 0.3s ease;
        }

        .category-btn:hover {
            transform: translateY(-5px);
            box-shadow: 0 8px 12px rgba(0, 0, 0, 0.15);
            background: linear-gradient(135deg, #1A472A 0%, #0F3460 100%);
            color: white;
            border-color: #FFD700;
        }

        .category-btn.active {
            background: linear-gradient(135deg, #1A472A 0%, #0F3460 100%);
            color: white;
            border-color: #FFD700;
            box-shadow: 0 0 15px rgba(255, 215, 0, 0.3);
        }

        .adhkar-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
            gap: 1.5rem;
        }

        .adhkar-card {
            background: white;
            border-radius: 10px;
            padding: 1.5rem;
            box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
            transition: all 0.3s ease;
            display: none;
            border-top: 4px solid #FFD700;
        }

        .adhkar-card.active {
            display: block;
            animation: slideIn 0.3s ease;
        }

        @keyframes slideIn {
            from {
                opacity: 0;
                transform: translateY(10px);
            }
            to {
                opacity: 1;
                transform: translateY(0);
            }
        }

        .adhkar-card:hover {
            transform: translateY(-5px);
            box-shadow: 0 8px 12px rgba(255, 215, 0, 0.2);
            border-top-color: #1A472A;
        }

        .adhkar-title {
            color: #1A472A;
            font-size: 1.3rem;
            margin-bottom: 0.5rem;
            font-weight: 700;
            border-right: 4px solid #FFD700;
            padding-right: 0.5rem;
        }

        .adhkar-text {
            color: #333;
            line-height: 1.8;
            margin-bottom: 1rem;
            font-size: 1rem;
        }

        .adhkar-count {
            background: linear-gradient(135deg, #1A472A 0%, #0F3460 100%);
            color: white;
            padding: 0.5rem 1rem;
            border-radius: 20px;
            display: inline-block;
            font-size: 0.9rem;
        }

        .adhkar-details {
            background: #f5f9fb;
            border-right: 4px solid #FFD700;
            padding: 1rem;
            margin-top: 1rem;
            border-radius: 5px;
            font-size: 0.95rem;
            color: #1A472A;
            line-height: 1.7;
        }

        .adhkar-hadith {
            background: #e8f4f8;
            padding: 0.8rem;
            margin-top: 0.5rem;
            border-radius: 5px;
            font-style: italic;
            color: #0F3460;
            font-size: 0.9rem;
            border-left: 3px solid #FFD700;
            padding-right: 0.8rem;
        }

        .adhkar-benefit {
            background: #f0f8f4;
            padding: 0.8rem;
            margin-top: 0.5rem;
            border-radius: 5px;
            color: #1A472A;
            font-size: 0.9rem;
            border-left: 3px solid #FFD700;
            padding-right: 0.8rem;
        }

        .copy-btn {
            background: linear-gradient(135deg, #1A472A 0%, #0F3460 100%);
            color: white;
            border: none;
            padding: 0.5rem 1rem;
            border-radius: 5px;
            cursor: pointer;
            margin-right: 0.5rem;
            transition: all 0.3s ease;
        }

        .copy-btn:hover {
            background: linear-gradient(135deg, #0F3460 0%, #1A472A 100%);
            box-shadow: 0 0 10px rgba(255, 215, 0, 0.3);
        }

        .counter-section {
            background: linear-gradient(135deg, #1A472A 0%, #0F3460 50%, #16213E 100%);
            padding: 1.5rem;
            border-radius: 10px;
            margin-top: 1rem;
            text-align: center;
            color: white;
            border: 2px solid #FFD700;
        }

        .counter-display {
            font-size: 3rem;
            font-weight: 700;
            margin: 1rem 0;
            text-shadow: 2px 2px 4px rgba(0, 0, 0, 0.2);
        }

        .counter-label {
            font-size: 1rem;
            margin-bottom: 1rem;
            opacity: 0.9;
        }

        .counter-buttons {
            display: flex;
            gap: 0.5rem;
            justify-content: center;
            flex-wrap: wrap;
        }

        .increment-btn {
            background: linear-gradient(135deg, #FFD700 0%, #DCA408 100%);
            color: #1A472A;
            border: none;
            padding: 0.75rem 1.5rem;
            border-radius: 25px;
            cursor: pointer;
            font-size: 1rem;
            font-weight: 600;
            transition: all 0.3s ease;
            box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
        }

        .increment-btn:hover {
            transform: scale(1.05);
            box-shadow: 0 6px 12px rgba(255, 215, 0, 0.4);
        }

        .reset-btn {
            background: rgba(255, 215, 0, 0.15);
            color: #FFD700;
            border: 2px solid #FFD700;
            padding: 0.75rem 1.5rem;
            border-radius: 25px;
            cursor: pointer;
            font-size: 1rem;
            font-weight: 600;
            transition: all 0.3s ease;
        }

        .reset-btn:hover {
            background: #FFD700;
            color: #1A472A;
        }

        .footer {
            text-align: center;
            color: white;
            padding: 2rem;
            margin-top: 3rem;
            background: linear-gradient(135deg, rgba(15, 52, 96, 0.9) 0%, rgba(26, 71, 42, 0.9) 50%, rgba(22, 33, 62, 0.9) 100%);
            border-top: 3px solid #FFD700;
            position: relative;
        }

        .footer::before {
            content: '✦';
            display: block;
            font-size: 1.5rem;
            color: #FFD700;
            margin-bottom: 0.5rem;
        }

        @media (max-width: 768px) {
            .header h1 {
                font-size: 1.8rem;
            }
            .categories {
                grid-template-columns: 1fr;
            }
            .adhkar-grid {
                grid-template-columns: 1fr;
            }
        }
    </style>
</head>
<body>
    <div class="header">
        <h1>🌙 اذكار المسلم</h1>
        <p>مجموعة شاملة من الأذكار والأدعية الإسلامية</p>
    </div>

    <div class="container">
        <div class="search-bar">
            <input type="text" id="searchInput" placeholder="ابحث عن ذكر...">
        </div>

        <div class="categories">
            <button class="category-btn active" onclick="filterCategory('all')">الكل</button>
            <button class="category-btn" onclick="filterCategory('adhkar')">🌙 الأذكار</button>
            <button class="category-btn" onclick="filterCategory('dua')">🤲 الأدعية</button>
            <button class="category-btn" onclick="filterCategory('morning')">أذكار الصباح</button>
            <button class="category-btn" onclick="filterCategory('evening')">أذكار المساء</button>
            <button class="category-btn" onclick="filterCategory('sleep')">أذكار النوم</button>
            <button class="category-btn" onclick="filterCategory('after-prayer')">أذكار بعد الصلاة</button>
            <button class="category-btn" onclick="filterCategory('entering-home')">أذكار الدخول والخروج</button>
            <button class="category-btn" onclick="filterCategory('daily')">أذكار يومية</button>
            <button class="category-btn" onclick="filterCategory('quran')">آيات قرآنية</button>
        </div>

        <div class="adhkar-grid" id="adhkarGrid">
            <!-- سيتم ملء هذا الجزء بواسطة JavaScript -->
        </div>
    </div>

    <div class="footer">
        <p>&copy; 2026 موقع اذكار المسلم جزي الله العامل عليه خيرا اً</p>
        <p style="margin-top: 1rem; font-size: 0.95rem; opacity: 0.9;">
            📱 تصميم وتطوير: <strong>عمر احمد</strong> | الهاتف: <a href="tel:01146780736" style="color: white; text-decoration: none;">01146780736</a>
        </p>
    </div>

    <script>
        const adhkarData = [
            // أذكار الصباح
            {
                id: 1,
                type: 'adhkar',
                category: 'morning',
                title: 'قراءة آية الكرسي',
                text: 'اللَّهُ لا إِلَهَ إِلاَّ هُوَ الْحَيُّ الْقَيُّومُ ۚ لا تَأْخُذُهُ سِنَةٌ وَلا نَوْمٌ ۚ لَهُ مَا فِي السَّمَاوَاتِ وَمَا فِي الْأَرْضِ',
                count: 'مرة واحدة',
                hadith: 'عن أبي هريرة أن النبي ﷺ قال: «من قرأ آية الكرسي دبر كل صلاة لم يمنعه من دخول الجنة إلا أن يموت»',
                benefit: 'حفظ من الشياطين والسوء، وآية عظيمة فيها توحيد وقدرة الله'
            },
            {
                id: 2,
                type: 'adhkar',
                category: 'morning',
                title: 'سبحان الله وبحمده',
                text: 'سُبْحَانَ اللَّهِ وَبِحَمْدِهِ سُبْحَانَ اللَّهِ الْعَظِيمِ',
                count: '100 مرة',
                hadith: 'عن عبدالله بن عمر قال: قال رسول الله ﷺ: «من قال سبحان الله وبحمده في يوم مائة مرة حطت خطاياه وإن كانت مثل زبد البحر»',
                benefit: 'تُذهب الذنوب والخطايا، وتملأ الميزان'
            },
            {
                id: 3,
                type: 'adhkar',
                category: 'morning',
                title: 'لا إله إلا الله',
                text: 'لا إِلَهَ إِلاَّ اللَّهُ وَحْدَهُ لا شَرِيكَ لَهُ لَهُ الْمُلْكُ وَلَهُ الْحَمْدُ وَهُوَ عَلَى كُلِّ شَيْءٍ قَدِيرٌ',
                count: '10 مرات',
                hadith: 'عن سمرة بن جندب قال: قال رسول الله ﷺ: «من قال في صباح كل يوم لا إله إلا الله وحده لا شريك له له الملك وله الحمد وهو على كل شيء قدير مائة مرة كان حرزاً له من الشيطان طول يومه»',
                benefit: 'حفظ من الشيطان وحصن قوي للنفس'
            },
            {
                id: 4,
                type: 'adhkar',
                category: 'morning',
                title: 'أستغفر الله',
                text: 'أَسْتَغْفِرُ اللَّهَ وَأَتُوبُ إِلَيْهِ',
                count: '7 مرات فأكثر',
                hadith: 'عن شداد بن أوس قال: قال رسول الله ﷺ: «من استغفر الله سبعين مرة كتب الله له براءة»',
                benefit: 'تطهير النفس من الذنوب والمعاصي، وتوبة نصوحة إلى الله'
            },
            {
                id: 5,
                type: 'adhkar',
                category: 'morning',
                title: 'الحمد لله رب العالمين',
                text: 'الْحَمْدُ لِلَّهِ رَبِّ الْعَالَمِينَ أَحْمَدُهُ حَمْداً كَثِيراً طَيِّباً مُبَارَكاً فِيهِ',
                count: 'عدة مرات',
                hadith: 'أن النبي ﷺ كان يستفتح دعاءه بحمد الله والثناء عليه',
                benefit: 'تذكر نعم الله وشكره، وتزكية النفس'
            },
            // أذكار المساء
            {
                id: 6,
                type: 'adhkar',
                category: 'evening',
                title: 'أمسينا وأمسى الملك',
                text: 'أَمْسَيْنَا وَأَمْسَى الْمُلْكُ لِلَّهِ، وَالْحَمْدُ لِلَّهِ، لا إِلَهَ إِلاَّ اللَّهُ وَحْدَهُ لا شَرِيكَ لَهُ، لَهُ الْمُلْكُ وَلَهُ الْحَمْدُ وَهُوَ عَلَى كُلِّ شَيْءٍ قَدِيرٌ',
                count: '3 مرات',
                hadith: 'عن عبدالله بن مسعود رضي الله عنه أن النبي ﷺ أوصاه بهذا الذكر',
                benefit: 'التسليم لله بالملك، وتذكر قدرته سبحانه'
            },
            {
                id: 7,
                type: 'dua',
                category: 'evening',
                title: 'اللهم إني أعوذ بك',
                text: 'اللَّهُمَّ إِنِّي أَعُوذُ بِكَ مِنْ شَرِّ سَمْعِي وَشَرِّ بَصَرِي وَشَرِّ لِسَانِي وَشَرِّ قَلْبِي وَشَرِّ مَنِيِّي',
                count: 'مرة واحدة أو أكثر',
                hadith: 'عن ابن عمر رضي الله عنهما عن النبي ﷺ',
                benefit: 'الاستعاذة من شرور الجوارح والقلب'
            },
            {
                id: 8,
                type: 'dua',
                category: 'evening',
                title: 'اللهم ما أمسى وأصبح بي من نعمة',
                text: 'اللَّهُمَّ مَا أَمْسَىٰ بِي مِنْ نِعْمَةٍ فَمِنْكَ وَحْدَكَ لا شَرِيكَ لَكَ، فَلَكَ الْحَمْدُ وَلَكَ الشُّكْرُ',
                count: 'مرة واحدة',
                hadith: 'دعاء نبوي كريم للشكر على النعم',
                benefit: 'شكر الله على نعمه ورحمته'
            },
            {
                id: 9,
                category: 'evening',
                title: 'الحزم والأمان في المساء',
                text: 'بِسْمِ اللَّهِ الذي لا يضر مع اسمه شيء في الأرض ولا في السماء وهو السميع العليم',
                count: '3 مرات',
                hadith: 'عن خولة بنت حكيم رضي الله عنها عن النبي ﷺ',
                benefit: 'حفظ شامل من كل شر في الأرض والسماء'
            },
            // أذكار النوم
            {
                id: 10,
                category: 'sleep',
                title: 'دعاء النوم الكامل',
                text: 'اللَّهُمَّ أَسْلَمْتُ وَجْهِي إِلَيْكَ، وَفَوَّضْتُ أَمْرِي إِلَيْكَ، وَأَلْجَأْتُ ظَهْرِي إِلَيْكَ، رَغْبَةً وَرَهْبَةً إِلَيْكَ، لا مَلْجَأَ وَلا مَنْجَىٰ مِنْكَ إِلاَّ إِلَيْكَ، آمَنتُ بِكِتَابِكَ الذي أَنزَلْتَ، وَبِنَبِيِّكَ الذي أَرْسَلْتَ',
                count: 'قبل النوم مباشرة',
                hadith: 'عن البراء بن عازب قال: قال لي رسول الله ﷺ: «إذا أتيت مضجعك فتوضأ وضوءك للصلاة ثم اضطجع على شقك الأيمن ثم قل...»',
                benefit: 'استسلام كامل لله تعالى، وتوكل عليه قبل النوم'
            },
            {
                id: 11,
                category: 'sleep',
                title: 'بسمك اللهم أموت وأحيا',
                text: 'بِسْمِكَ اللَّهُمَّ أَمُوتُ وَأَحْيَا',
                count: 'قبل النوم',
                hadith: 'عن حفصة أم المؤمنين قالت: لما أراد النبي ﷺ أن ينام قال هذا الدعاء',
                benefit: 'التسليم إلى الله بموت النوم وحياة الاستيقاظ'
            },
            {
                id: 12,
                category: 'sleep',
                title: 'سبحان الله ثلاثاً وثلاثين',
                text: 'سُبْحَانَ اللَّهِ (33 مرة)، وَالْحَمْدُ لِلَّهِ (33 مرة)، وَاللَّهُ أَكْبَرُ (34 مرة)',
                count: 'قبل النوم أو التوضي',
                hadith: 'عن علي رضي الله عنه قال: أوصاني النبي ﷺ بهذا الذكر',
                benefit: 'تطهير النفس والقلب قبل النوم'
            },
            // أذكار بعد الصلاة
            {
                id: 13,
                category: 'after-prayer',
                title: 'التسبيح والتكبير والتحميد',
                text: 'سُبْحَانَ اللَّهِ وَالْحَمْدُ لِلَّهِ وَاللَّهُ أَكْبَرُ',
                count: '33 مرة لكل واحد',
                hadith: 'عن أبي هريرة قال: بخ بخ لشيخين من الأنصار قالا هذا التسبيح',
                benefit: 'تسبيح الملائكة وتعظيم الله بعد فرائضه'
            },
            {
                id: 14,
                category: 'after-prayer',
                title: 'استغفر الله ثلاثاً',
                text: 'أَسْتَغْفِرُ اللَّهَ (3 مرات) + اللَّهُمَّ أَنْتَ السَّلاَمُ وَمِنْكَ السَّلاَمُ تَبَارَكْتَ يَا ذَا الْجَلاَلِ وَالإِكْرَامِ',
                count: 'بعد كل صلاة مباشرة',
                hadith: 'عن ابن عمر رضي الله عنهما أن النبي ﷺ كان يفعل هذا',
                benefit: 'الاستغفار والدعاء بالسلام والتبارك'
            },
            // أذكار الدخول والخروج
            {
                id: 15,
                category: 'entering-home',
                title: 'الدخول إلى المنزل',
                text: 'بِسْمِ اللَّهِ وَلَجْنَا وَبِسْمِ اللَّهِ خَرَجْنَا وَعَلَى اللَّهِ رَبِّنَا تَوَكَّلْنَا',
                count: 'عند الدخول والخروج',
                hadith: 'السنة أن يذكر الله عند الدخول والخروج من المنزل',
                benefit: 'تذكر الله في كل تنقل وحركة'
            },
            {
                id: 16,
                category: 'entering-home',
                title: 'دعاء رؤية الهلال',
                text: 'اللَّهُمَّ أَهِلَّهُ عَلَيْنَا بِالْأَمْنِ وَالإِيمَانِ، وَالسَّلاَمَةِ وَالإِسْلاَمِ، وَالتَّوْفِيقِ لِمَا تُحِبُّ وَتَرْضَىٰ رَبّنَا وَرَبُّ الهِلاَلِ، الْحَمْدُ لِلَّهِ الّذِي ذَهَبَ بِشَهْرِ كَذَا وَجَاءَ بِشَهْرِ كَذَا',
                count: 'عند رؤية الهلال',
                hadith: 'عن طلحة بن عبيدالله قال: رأيت النبي ﷺ يقول هذا',
                benefit: 'الدعاء بالخير وطلب الأمن والإيمان'
            },
            {
                id: 17,
                category: 'entering-home',
                title: 'دعاء الخروج من المنزل',
                text: 'أَعُوذُ بِاللَّهِ مِنْ أَنْ أَضِلَّ أَوْ أُضَلَّ، أَوْ أَزِلَّ أَوْ أُزَلَّ، أَوْ أَظْلِمَ أَوْ أُظْلَمَ، أَوْ أَجْهَلَ أَوْ يُجْهَلَ عَليّ',
                count: 'عند الخروج',
                hadith: 'عن ابن عمر رضي الله عنهما',
                benefit: 'الحفظ من الضلالة والزلل والظلم والجهل'
            },
            // أذكار يومية
            {
                id: 18,
                category: 'daily',
                title: 'دعاء الطريق',
                text: 'اللَّهُمَّ إِنِّي أَسْأَلُكَ خَيْرَ هَذِهِ اللَّيْلَةِ قَمَرُهَا وَنُجُومُهَا وَرِيحُهَا وَمَطَرُهَا وَسَائِرَ خَيْرِهَا وَأَعُوذُ بِكَ مِنْ شَرِّهَا وَشَرِّ مَا فِيهَا',
                count: 'عند المشي في الطريق',
                hadith: 'دعاء نبوي للخير والحفظ',
                benefit: 'طلب الخير من الليل والنهار والحفظ من الشر'
            },
            {
                id: 19,
                category: 'daily',
                title: 'الاستعاذة من الشيطان',
                text: 'أَعُوذُ بِاللَّهِ مِنَ الشَّيْطَانِ الرَّجِيمِ',
                count: 'حسب الحاجة',
                hadith: 'الاستعاذة من الشيطان الرجيم من السنة وقول القرآن',
                benefit: 'حفظ من وسوسة الشيطان وإغواؤه'
            },
            {
                id: 20,
                category: 'daily',
                title: 'الصبر والتوكل',
                text: 'حَسْبُنَا اللَّهُ وَنِعْمَ الْوَكِيلُ',
                count: 'عند الشدة والضيق',
                hadith: 'قال الله تعالى في القرآن: (حسبنا الله ونعم الوكيل)',
                benefit: 'القناعة والتوكل على الله تعالى'
            },
            {
                id: 21,
                category: 'daily',
                title: 'ما شاء الله',
                text: 'مَا شَاءَ اللَّهُ لا قُوَّةَ إِلاَّ بِاللَّهِ',
                count: 'عند رؤية ما يعجب',
                hadith: 'دعاء الحفظ من العين عند الإعجاب بالشيء',
                benefit: 'الحفظ من العين والحسد'
            },
            // آيات قرآنية
            {
                id: 22,
                category: 'quran',
                title: 'سورة الإخلاص',
                text: 'قُلْ هُوَ اللَّهُ أَحَدٌ * اللَّهُ الصَّمَدُ * لَمْ يَلِدْ وَلَمْ يُولَدْ * وَلَمْ يَكُنْ لَهُ كُفُوًا أَحَدٌ',
                count: '3 مرات',
                hadith: 'قال رسول الله ﷺ: (من قرأ قل هو الله أحد ثلاث مرات فقد قرأ القرآن)',
                benefit: 'توحيد الله والعظمة والكمال'
            },
            {
                id: 23,
                category: 'quran',
                title: 'المعوذتان',
                text: 'قُلْ أَعُوذُ بِرَبِّ الْفَلَقِ * مِنْ شَرِّ مَا خَلَقَ * وَمِنْ شَرِّ غَاسِقٍ إِذَا وَقَبَ * وَمِنْ شَرِّ النَّفَّاثَاتِ فِي الْعُقَدِ * وَمِنْ شَرِّ حَاسِدٍ إِذَا حَسَدَ',
                count: '3 مرات',
                hadith: 'قال رسول الله ﷺ: (قلت قل أعوذ برب الفلق والمعوذتان)',
                benefit: 'حفظ شامل من كل شر'
            },
            {
                id: 24,
                category: 'quran',
                title: 'سورة الفاتحة',
                text: 'بِسْمِ اللَّهِ الرَّحْمَٰنِ الرَّحِيمِ * الْحَمْدُ لِلَّهِ رَبِّ الْعَالَمِينَ * الرَّحْمَٰنِ الرَّحِيمِ * مَالِكِ يَوْمِ الدِّينِ',
                count: 'في كل صلاة',
                hadith: 'قال النبي ﷺ: (الحمد لله رب العالمين هي أم الكتاب)',
                benefit: 'أعظم سورة في القرآن الكريم'
            },
            {
                id: 25,
                category: 'quran',
                title: 'آية الكرسي',
                text: 'اللَّهُ لا إِلَهَ إِلاَّ هُوَ الْحَيُّ الْقَيُّومُ ۚ لا تَأْخُذُهُ سِنَةٌ وَلا نَوْمٌ ۚ لَهُ مَا فِي السَّمَاوَاتِ وَمَا فِي الْأَرْضِ ۚ مَنْ ذَا الَّذِي يَشْفَعُ عِنْدَهُ إِلاَّ بِإِذْنِهِ',
                count: 'مرة واحدة أو أكثر',
                hadith: 'أفضل آية في كتاب الله - آية الكرسي',
                benefit: 'حفظ عظيم وتوحيد وقدرة الله'
            },
            // أذكار إضافية
            {
                id: 26,
                category: 'morning',
                title: 'إذا أصبحنا وأصبح الملك',
                text: 'إِذَا أَصْبَحْنَا وَأَصْبَحَ الْمُلْكُ لِلَّهِ، وَالْحَمْدُ لِلَّهِ، لا إِلَهَ إِلاَّ اللَّهُ وَحْدَهُ لا شَرِيكَ لَهُ، لَهُ الْمُلْكُ وَلَهُ الْحَمْدُ وَهُوَ عَلَى كُلِّ شَيْءٍ قَدِيرٌ',
                count: '3 مرات',
                hadith: 'عن ابن مسعود رضي الله عنه عن النبي ﷺ',
                benefit: 'تسليم الملك لله وشكره على نعمه'
            },
            {
                id: 27,
                category: 'morning',
                title: 'دعاء الاستيقاظ من النوم',
                text: 'اَلْحَمْدُ لِلَّهِ الَّذِي أَحْيَانَا بَعْدَ مَا أَمَاتَنَا وَإِلَيْهِ النُّشُورُ',
                count: 'عند الاستيقاظ',
                hadith: 'عن أبي موسى الأشعري رضي الله عنه',
                benefit: 'شكر الله على إحياء النفس والحياة'
            },
            {
                id: 28,
                category: 'entering-home',
                title: 'دعاء دخول الحمام',
                text: 'اَللَّهُمَّ إِنِّي أَعُوذُ بِكَ مِنَ الْخُبُثِ وَالْخَبَائِثِ',
                count: 'عند دخول الحمام',
                hadith: 'عن أنس بن مالك رضي الله عنه',
                benefit: 'الاستعاذة من الشر والأذى'
            },
            {
                id: 29,
                category: 'daily',
                title: 'دعاء نزول المطر',
                text: 'اَللَّهُمَّ اسْقِنَا غَيْثاً مُغِيثاً مَرِيعاً مُنَبِّتاً نَافِعاً غَيْرَ ضَارٍّ',
                count: 'عند هبوب الريح والمطر',
                hadith: 'عن ابن عباس رضي الله عنهما',
                benefit: 'طلب الغيث والبركة من الله'
            },
            {
                id: 30,
                category: 'daily',
                title: 'دعاء الخروج من المسجد',
                text: 'اَللَّهُمَّ اجْعَلْ أَوَّلَ خُرُوجِي هَذَا لِلْعِتْقِ مِنَ النَّارِ، وَارْزُقْنِي فِيهِ رِضْوَانَكَ وَأَيِّدْنِي عَلَى طَاعَتِكَ',
                count: 'عند الخروج من المسجد',
                hadith: 'دعاء من الأدعية المأثورة',
                benefit: 'طلب العتق من النار والرضا من الله'
            },
            {
                id: 31,
                category: 'evening',
                title: 'دعاء المساء الشامل',
                text: 'أَمْسَيْنَا وَأَمْسَى مُلْكُ اللَّهِ بِخَيْرٍ، اَللَّهُمَّ إِنِّي أَسْأَلُكَ خَيْرَ هَذِهِ اللَّيْلَةِ وَخَيْرَ مَا فِيهَا',
                count: 'مرة واحدة أو أكثر',
                hadith: 'من أدعية السنة النبوية',
                benefit: 'حماية وبركة طوال الليل'
            },
            {
                id: 32,
                category: 'daily',
                title: 'دعاء لبس الثياب',
                text: 'اَلْحَمْدُ لِلَّهِ الَّذِي كَسَانِي هَذَا وَرَزَقَنِيهِ مِنْ غَيْرِ حَوْلٍ مِنِّي وَلا قُوَّةٍ',
                count: 'عند لبس الثوب الجديد',
                hadith: 'عن أبي سعيد الخدري رضي الله عنه',
                benefit: 'شكر الله على النعم واللباس'
            },
            {
                id: 33,
                category: 'sleep',
                title: 'دعاء قبل النوم - الإمام أحمد',
                text: 'اَللَّهُمَّ بِاسْمِكَ أَمُوتُ وَأَحْيَا',
                count: 'قبل النوم',
                hadith: 'عن حفصة أم المؤمنين',
                benefit: 'التسليم الكامل لله قبل النوم'
            },
            {
                id: 34,
                category: 'after-prayer',
                title: 'لا حول ولا قوة إلا بالله',
                text: 'لا حَوْلَ وَلا قُوَّةَ إِلاَّ بِاللَّهِ الْعَلِيِّ الْعَظِيمِ',
                count: '10 مرات',
                hadith: 'عن أبي موسى الأشعري رضي الله عنه قال: قال النبي ﷺ: ألا أدلك على كلمة من كنوز الجنة؟',
                benefit: 'كنز من كنوز الجنة والتوكل على الله'
            },
            {
                id: 35,
                category: 'quran',
                title: 'سورة الناس',
                text: 'قُلْ أَعُوذُ بِرَبِّ النَّاسِ * مَلِكِ النَّاسِ * إِلَهِ النَّاسِ * مِنْ شَرِّ الْوَسْوَاسِ الْخَنَّاسِ * الَّذِي يُوَسْوِسُ فِي صُدُورِ النَّاسِ * مِنَ الْجِنَّةِ وَالنَّاسِ',
                count: '3 مرات',
                hadith: 'من المعوذتين مع سورة الإخلاص والفلق',
                benefit: 'حماية من الوسوسة والشياطين'
            },
            {
                id: 36,
                category: 'daily',
                title: 'اللهم صل على محمد',
                text: 'اَللَّهُمَّ صَلِّ عَلَى مُحَمَّدٍ وَعَلَى آلِ مُحَمَّدٍ كَمَا صَلَّيْتَ عَلَى إِبْرَاهِيمَ وَعَلَى آلِ إِبْرَاهِيمَ، إِنَّكَ حَمِيدٌ مَجِيدٌ',
                count: 'عدة مرات',
                hadith: 'من أفضل الأذكار والدعوات كما قال النبي ﷺ',
                benefit: 'الصلاة على النبي ﷺ وشرفه والبركة'
            },
            {
                id: 37,
                category: 'morning',
                title: 'دعاء سيدنا إبراهيم',
                text: 'رَبِّ اجْعَلْ هَذَا الْبَلَدَ آمِناً وَارْزُقْ أَهْلَهُ مِنَ الثَّمَرَاتِ مَنْ آمَنَ مِنْهُمْ بِاللَّهِ وَالْيَوْمِ الْآخِرِ',
                count: 'مرة واحدة أو أكثر',
                hadith: 'من دعاء إبراهيم عليه السلام',
                benefit: 'طلب الأمن والرزق للبلاد والعباد'
            },
            {
                id: 38,
                category: 'evening',
                title: 'اللهم بك أصبحنا',
                text: 'اَللَّهُمَّ بِكَ أَمْسَيْنَا، وَبِكَ أَصْبَحْنَا، وَبِكَ نَحْيَا، وَبِكَ نَمُوتُ، وَإِلَيْكَ النُّشُورُ',
                count: 'مرة واحدة',
                hadith: 'من أدعية السنة النبوية',
                benefit: 'التوكل على الله في جميع الأحوال'
            },
            {
                id: 39,
                category: 'daily',
                title: 'سبحان الله وبحمده سبحان الله العظيم',
                text: 'سُبْحَانَ اللَّهِ وَبِحَمْدِهِ سُبْحَانَ اللَّهِ الْعَظِيمِ، أَسْتَغْفِرُ اللَّهَ وَأَتُوبُ إِلَيْهِ',
                count: 'عدة مرات يومياً',
                hadith: 'من أفضل الأذكار التي تملأ الميزان',
                benefit: 'تطهير الذنوب وملء الميزان بالحسنات'
            },
            {
                id: 40,
                category: 'quran',
                title: 'آيات السجدة',
                text: 'إِنَّ الَّذِينَ آمَنُوا يُؤْمِنُونَ بِهِ وَرَحْمَةُ رَبِّكَ تَسَعُ كُلَّ شَيْءٍ',
                count: 'عند التأمل',
                hadith: 'من أعظم الآيات القرآنية',
                benefit: 'الإيمان والدعوة إلى الله برحمته'
            },
            {
                id: 41,
                category: 'daily',
                title: 'دعاء الذهاب للسوق',
                text: 'اَللَّهُمَّ إِنِّي أَعُوذُ بِكَ مِنْ أَنْ أَظْلِمَ أَوْ أُظْلَمَ، أَوْ أَعْتَدِيَ أَوْ يُعْتَدَى عَليَّ',
                count: 'عند الذهاب للسوق',
                hadith: 'من أدعية الانتقال',
                benefit: 'حفظ من الظلم والعدوان'
            },
            {
                id: 42,
                category: 'sleep',
                title: 'استقل بربك',
                text: 'لا إِلَهَ إِلاَّ اللَّهُ وَحْدَهُ لا شَرِيكَ لَهُ، لَهُ الْمُلْكُ وَلَهُ الْحَمْدُ، وَهُوَ عَلَى كُلِّ شَيْءٍ قَدِيرٌ',
                count: 'قبل النوم',
                hadith: 'من أدعية القلب والصدر',
                benefit: 'هدوء النفس والسلام قبل النوم'
            },
            {
                id: 43,
                category: 'after-prayer',
                title: 'الاستغفار والتعقيب بعد الصلاة',
                text: 'أَسْتَغْفِرُ اللَّهَ ثلاثا، اللَّهُمَّ أَنْتَ السَّلاَمُ وَمِنْكَ السَّلاَمُ، تَبَارَكْتَ يَا ذَا الْجَلاَلِ وَالْإِكْرَامِ',
                count: 'بعد كل صلاة',
                hadith: 'من تعقيب الصلوات المأثور',
                benefit: 'تطهير من الذنوب والسلام من الله'
            },
            {
                id: 44,
                category: 'morning',
                title: 'دعاء طلوع الشمس',
                text: 'اَللَّهُمَّ بِبَرَكَةِ هَذَا الصَّبَاحِ وَنُورِ الشَّمْسِ اجْعَلْ يَومِي خَيْرًا',
                count: 'عند الفجر',
                hadith: 'من أدعية الصباح',
                benefit: 'بركة اليوم وخيره'
            },
            {
                id: 45,
                category: 'evening',
                title: 'دعاء الغروب',
                text: 'اَللَّهُمَّ بِظُلامِ هَذِهِ اللَّيْلَةِ أَسْأَلُكَ السَّتْرَ وَالْحِفْظَ وَالْأَمْنَ',
                count: 'عند الغروب',
                hadith: 'من أدعية المساء',
                benefit: 'الأمن والحفظ طول الليل'
            },
            {
                id: 46,
                category: 'daily',
                title: 'دعاء الدخول إلى السوق',
                text: 'بِسْمِ اللَّهِ، لا إِلَهَ إِلاَّ اللَّهُ وَحْدَهُ لا شَرِيكَ لَهُ، لَهُ الْمُلْكُ وَلَهُ الْحَمْدُ، يُحْيِي وَيُمِيتُ',
                count: 'عند الدخول',
                hadith: 'من أدعية الحركة والانتقال',
                benefit: 'تسليم من الله عند البيع والشراء'
            },
            {
                id: 47,
                category: 'daily',
                title: 'دعاء الرياح',
                text: 'اَللَّهُمَّ إِنِّي أَسْأَلُكَ خَيْرَ هَذِهِ الرِّيحِ وَخَيْرَ مَا فِيهَا وَخَيْرَ مَا أُرْسِلَتْ بِهِ',
                count: 'عند هبوب الريح',
                hadith: 'عن أم المؤمنين عائشة',
                benefit: 'طلب الخير من الله في الريح'
            },
            {
                id: 48,
                category: 'entering-home',
                title: 'دعاء الدخول إلى الدار',
                text: 'بِسْمِ اللَّهِ دَخَلْنَا وَبِسْمِ اللَّهِ خَرَجْنَا وَعَلَى رَبِّنَا تَوَكَّلْنَا',
                count: 'عند الدخول والخروج',
                hadith: 'من سنن الانتقال والحركة',
                benefit: 'البركة والحفظ في المنزل'
            },
            {
                id: 49,
                category: 'quran',
                title: 'سورة الفيل',
                text: 'أَلَمْ تَرَ كَيْفَ فَعَلَ رَبُّكَ بِأَصْحَابِ الْفِيلِ * أَلَمْ يَجْعَلْ كَيْدَهُمْ فِي تَضْلِيلٍ',
                count: 'مرة أو أكثر',
                hadith: 'من سور القرآن الكريم',
                benefit: 'حفظ الله وقوته على أعدائه'
            },
            {
                id: 50,
                category: 'after-prayer',
                title: 'دعاء الفراغ من الصلاة',
                text: 'اَللَّهُمَّ مِنْ قَبْلِكَ جَاءَتْ وَإِلَيْكَ تَعُودُ، اَللَّهُمَّ تَقَبَّلْ مِنِّي',
                count: 'بعد الصلاة مباشرة',
                hadith: 'من أدعية ما بعد الصلوات',
                benefit: 'قبول الصلاة من الله'
            },
            {
                id: 51,
                category: 'morning',
                title: 'دعاء المجلس',
                text: 'سُبْحَانَكَ اللَّهُمَّ وَبِحَمْدِكَ أَشْهَدُ أَنْ لا إِلَهَ إِلاَّ أَنْتَ، أَسْتَغْفِرُكَ وَأَتُوبُ إِلَيْكَ',
                count: 'قبل القيام من المجلس',
                hadith: 'من آداب الجلسة',
                benefit: 'كفارة الجلسة من الآثام'
            },
            {
                id: 52,
                category: 'daily',
                title: 'دعاء قضاء الحاجة',
                text: 'اَللَّهُمَّ إِنِّي أَسْأَلُكَ بِرَحْمَتِكَ الَّتِي وَسِعَتْ كُلَّ شَيْءٍ أَنْ تَقْضِيَ لِي حَاجَتِي',
                count: 'عند الحاجة',
                hadith: 'من أدعية قضاء الحوائج',
                benefit: 'تيسير الحوائج والدعاء'
            },
            {
                id: 53,
                category: 'evening',
                title: 'دعاء تجديد النية',
                text: 'اَللَّهُمَّ إِنَّ نِيَّتِي غَدًا الله، اَللَّهُمَّ وَفِّقْنِي لِمَا تُحِبُّ وَتَرْضَىٰ',
                count: 'قبل النوم',
                hadith: 'من أدعية جديدة النية',
                benefit: 'تصحيح النية وطلب التوفيق'
            },
            {
                id: 54,
                category: 'quran',
                title: 'سورة الفلق',
                text: 'قُلْ أَعُوذُ بِرَبِّ الْفَلَقِ * مِنْ شَرِّ مَا خَلَقَ * وَمِنْ شَرِّ غَاسِقٍ إِذَا وَقَبَ',
                count: '3 مرات',
                hadith: 'من المعوذات العظيمة',
                benefit: 'أعوذ بالله من شرور مختلفة'
            },
            {
                id: 55,
                category: 'daily',
                title: 'اللهم اهدني',
                text: 'اَللَّهُمَّ اهْدِنِي لأَحْسَنِ الأَخْلاقِ لا يَهْدِي لأَحْسَنِهَا إِلا أَنْتَ، وَاصْرِفْ عَنِّي سَيِّئَهَا',
                count: 'عدة مرات',
                hadith: 'من دعاء النبي ﷺ',
                benefit: 'الهداية للأخلاق الحسنة'
            }
        ];

        // إضافة type تلقائياً للعناصر التي لا تحتوي عليه
        adhkarData.forEach(item => {
            if (!item.type) {
                const titleLower = item.title.toLowerCase();
                const textLower = item.text.toLowerCase();
                
                // تحديد ما إذا كان دعاء أو ذكر
                if (titleLower.includes('دعاء') || 
                    titleLower.includes('استعاذة') || 
                    titleLower.includes('شكر') ||
                    titleLower.includes('سؤال') ||
                    textLower.includes('دعاء') ||
                    textLower.includes('إني أسأل')) {
                    item.type = 'dua';
                } else if (item.category === 'quran') {
                    item.type = 'adhkar';
                } else {
                    // افتراضي - إذا كان يحتوي على "الل" في البداية فهو ذكر
                    item.type = textLower.startsWith('اللَّهُمَّ') ? 'dua' : 'adhkar';
                }
            }
        });

        let currentCategory = 'all';
        let currentType = 'all';

        function renderAdhkar() {
            const grid = document.getElementById('adhkarGrid');
            grid.innerHTML = '';

            let count = 0;
            adhkarData.forEach(adhkar => {
                let showCard = false;
                
                if (currentCategory === 'all' && currentType === 'all') {
                    showCard = true;
                } else if (currentType !== 'all' && adhkar.type === currentType) {
                    showCard = true;
                } else if (currentCategory !== 'all' && adhkar.category === currentCategory && currentType === 'all') {
                    showCard = true;
                }
                
                if (showCard) {
                    count++;
                    const card = document.createElement('div');
                    card.className = 'adhkar-card active';
                    card.innerHTML = `
                        <h3 class="adhkar-title">${count}. ${adhkar.title}</h3>
                        <p class="adhkar-text">${adhkar.text}</p>
                        <div class="adhkar-details">
                            <div><strong>📍 عدد المرات:</strong> ${adhkar.count}</div>
                            <div class="adhkar-hadith"><strong>📖 الحديث الشريف:</strong><br>${adhkar.hadith}</div>
                            <div class="adhkar-benefit"><strong>✨ الفضل والفائدة:</strong><br>${adhkar.benefit}</div>
                        </div>
                        <div class="counter-section">
                            <div class="counter-label">🔢 عداد الذكر</div>
                            <div class="counter-display" id="counter-${adhkar.id}">0</div>
                            <div class="counter-buttons">
                                <button class="increment-btn" onclick="incrementCounter(${adhkar.id})">➕ زيادة</button>
                                <button class="reset-btn" onclick="resetCounter(${adhkar.id})">🔄 إعادة تعيين</button>
                            </div>
                        </div>
                        <br>
                        <button class="copy-btn" onclick="copyToClipboard('${adhkar.text.replace(/'/g, "\\'")}')">📋 نسخ</button>
                        <button class="copy-btn" onclick="shareAdhkar('${adhkar.title}', '${adhkar.text.replace(/'/g, "\\'")}')">📤 شارك</button>
                    `;
                    grid.appendChild(card);
                }
            });
        }

        function filterCategory(category) {
            // Check if it's a type filter (adhkar or dua)
            if (category === 'adhkar' || category === 'dua') {
                currentType = category;
                currentCategory = 'all';
            } else {
                currentCategory = category;
                currentType = 'all';
            }
            
            // تحديث الأزرار النشطة
            document.querySelectorAll('.category-btn').forEach(btn => {
                btn.classList.remove('active');
            });
            event.target.classList.add('active');

            renderAdhkar();
        }

        function incrementCounter(id) {
            const counterElement = document.getElementById(`counter-${id}`);
            let currentValue = parseInt(localStorage.getItem(`adhkar-counter-${id}`) || '0');
            currentValue++;
            localStorage.setItem(`adhkar-counter-${id}`, currentValue);
            counterElement.textContent = currentValue;
        }

        function resetCounter(id) {
            const counterElement = document.getElementById(`counter-${id}`);
            localStorage.setItem(`adhkar-counter-${id}`, '0');
            counterElement.textContent = '0';
        }

        function loadCounterValue(id) {
            const counterElement = document.getElementById(`counter-${id}`);
            if (counterElement) {
                const savedValue = localStorage.getItem(`adhkar-counter-${id}`) || '0';
                counterElement.textContent = savedValue;
            }
        }

        function copyToClipboard(text) {
            navigator.clipboard.writeText(text).then(() => {
                alert('✅ تم نسخ الذكر بنجاح');
            });
        }

        function shareAdhkar(title, text) {
            const message = `🌙 ${title}\n\n${text}`;
            if (navigator.share) {
                navigator.share({
                    title: 'اذكار المسلم',
                    text: message
                });
            } else {
                copyToClipboard(message);
            }
        }

        // بحث
        document.getElementById('searchInput').addEventListener('keyup', function() {
            const searchTerm = this.value.toLowerCase();
            const cards = document.querySelectorAll('.adhkar-card');
            
            cards.forEach((card) => {
                const titleText = card.querySelector('.adhkar-title').textContent.toLowerCase();
                const bodyText = card.querySelector('.adhkar-text').textContent.toLowerCase();
                
                if (titleText.includes(searchTerm) || bodyText.includes(searchTerm)) {
                    card.style.display = 'block';
                } else {
                    card.style.display = 'none';
                }
            });
        });

        // تحميل البيانات في البداية
        renderAdhkar();

        // تحميل قيم العدادات المحفوظة
        setTimeout(() => {
            adhkarData.forEach(adhkar => {
                loadCounterValue(adhkar.id);
            });
        }, 100);
    </script>
</body>
</html>
