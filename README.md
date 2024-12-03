<!DOCTYPE html>
<html lang="ar">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>رسالة درجة الطالب</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            direction: rtl;
            text-align: right;
            margin: 20px;
        }
        .container {
            max-width: 600px;
            margin: auto;
            padding: 20px;
            border: 1px solid #ccc;
            border-radius: 10px;
            background-color: #f9f9f9;
        }
        label {
            font-weight: bold;
            margin-bottom: 5px;
        }
        input, button {
            width: 100%;
            padding: 10px;
            margin: 10px 0;
            border: 1px solid #ccc;
            border-radius: 5px;
        }
        button {
            background-color: #34495e;
            color: white;
            font-size: 16px;
            cursor: pointer;
        }
        button:hover {
            background-color: #2c3e50;
        }
        .message {
            margin-top: 20px;
            padding: 15px;
            border: 1px solid #4caf50;
            border-radius: 5px;
            background-color: #e8f5e9;
            color: #2e7d32;
        }
    </style>
</head>
<body>
    <div class="container">
        <h2>رسالة درجة الطالب</h2>
        
        <label for="studentCode">كود الطالب:</label>
        <input type="number" id="studentCode" placeholder="أدخل كود الطالب" oninput="fillStudentName()">
        
        <label for="studentName">اسم الطالب:</label>
        <input type="text" id="studentName" placeholder="اسم الطالب يظهر تلقائيًا" readonly>
        
        <label for="studentGrade">درجة الطالب:</label>
        <input type="number" id="studentGrade" placeholder="أدخل الدرجة من 60">
        
        <button onclick="generateMessage()">إنشاء الرسالة</button>
        
        <div id="result" class="message" style="display: none;"></div>
    </div>

    <script>
        const students = {
            "49696": "ادم عمرو",
            "81659": "نور عبدالرحمن",
            "39639": "ايمان محمد",
            "29474": "محمد ايهاب عبدالفتاح",
            "86074": "نيفين حمدي محمد",
            "30693": "رحمه ماجد",
            "25654": "اسلام محمد شعراوي",
            "50808": "احمد حسين",
            "84536": "زياد خالد",
            "41596": "نور الدين هيثم",
            "11633": "يوسف ايمن ابوضيف",
            "41715": "احمد حسام",
            "58471": "عبدالرحمن شعبان",
            "18054": "حنين السيد سليمان",
            "20321": "بسنت محمد",
            "52182": "عمر وليد جمال",
            "47916": "عبدالله احمد محمود",
            "35365": "حاتم امين محمد",
            "37144": "عبدالله احمد صلاح",
            "10781": "ياسمين السيد",
            "44889": "محمد سليم",
            "82128": "زياد ايهاب",
            "89303": "حمدي محمد",
            "80546": "مازن احمد سمير",
            "32546": "لوجين وائل",
            "23756": "ضحى محمد",
            "54620": "سلمى سامح",
            "67084": "هنا سعد",
            "16840": "سما ابراهيم",
            "15032": "تسنيم محمد",
            "88105": "سندي عصام",
            "72137": "رودينا ايمن",
            "80135": "محمد اشرف",
            "95731": "رودينا محمد نصر",
            "28126": "يوسف محمد",
            "56193": "حبيبة محمد",
            "75516": "حنين مصطفى",
            "53336": "مريم اشرف",
            "48389": "سندس صلاح",
            "92758": "مازن عبدالوهاب",
            "28354": "مريم احمد",
            "75539": "جنى طارق",
            "58951": "سارة عماد",
            "89089": "جنة محمد",
            "41292": "مريم سعيد",
            "32532": "مريم عاطف",
            "44746": "سعيد سعد",
            "30223": "سيف الدين تامر",
            "21428": "محمد احمد",
            "20608": "زياد احمد",
            "48392": "عمار اشرف",
            "16075": "امنية ايمن",
            "69897": "اروى احمد",
            "86284": "حبيبة شعبان",
            "73349": "محمود هشام",
            "80650": "احمد ايمن رافت",
            "25343": "يوسف محمود يحيي",
            "23069": "يوسف حسن محمد",
            "66908": "احمد محمد عبداللطيف",
            "69756": "احمد ياسر",
            "70126": "مازن محمد",
            "73057": "عمر هاني",
            "63855": "عبدالرحمن محمود عبدالحسيب",
            "46721": "ياسمين احمد محمود",
            "95464": "عمرو طارق",
            "06764": "زينب محمد علي",
            "28411": "رحيق سيد",
            "23849": "فرح عماد",
            "48261": "زياد احمد يوسف",
            "75934": "ضي عبدالعليم",
            "21687": "روان ايهاب",
            "25695": "فيرا عصام عدلي",
            "39472": "محمد عبدالعظيم",
            "58210": "سلمى وائل",
            "70493": "فيروز محمد",
            "50872": "ياسين الاعسر",
            "13856": "نورهان محمد",
            "94720": "سندس محمد",
            "58391": "ملك محمد",
            "35804": "ريم خالد",
            "62047": "منه الله جمال",
            "97510": "مهند خالد عبدالفتاح",
            "41729": "مؤمن ايهاب فؤاد",
            "15290": "محمد عمرو عبدالوهاب",
            "04596": "احمد سامح سعيد",
            "81463": "احمد ناجح",
            "85459": "يوسف محمد عبدالفتاح",
            "73431": "سلمى محمد السيد",
            "19153": "شهد سعيد",
            "41688": "اروى مصطفى",
            "94452": "دنيا كمال",
            "22030": "حبيبه احمد عبدالرؤوف",
            "68450": "ملك اشرف",
            "86554": "الاء محمود محمد",
            "64561": "ايه محمد نادي",
            "52434": "فارس ايمن سعد",
            "19734": "كريم عبدالمنعم محمد",
            "28417": "يوسف ابراهيم محمد",
            "56302": "ياسين محمد اسامه",
            "91846": "سارة عماد وجدي",
            "45176": "عبدالرحمن محمد محمود",
            "08724": "عبدالوهاب عبدالرحمن السيد"
        };

        function fillStudentName() {
            const code = document.getElementById('studentCode').value.trim();
            const studentNameInput = document.getElementById('studentName');
            studentNameInput.value = students[code] || ""; // إذا لم يتم العثور على الكود، يبقى الحقل فارغًا
        }

function generateMessage() {
    const name = document.getElementById('studentName').value.trim();
    const grade = document.getElementById('studentGrade').value.trim();
    const date = new Date().toLocaleDateString('ar-EG');
    const teacherName = "الباشمهندس/ طارق محمد";
    const contact = "01011717876";

    if (name === "" || grade === "") {
        alert("يرجى إدخال كود الطالب ودرجته.");
        return;
    }

    const message = `درجة الطالب ${name} ${grade} من 60 في امتحان الفيزياء على الفصل الثاني بتاريخ ${date}.\n${teacherName}\n..... للتواصل (واتساب): ${contact}`;
    const resultDiv = document.getElementById('result');
    resultDiv.textContent = message;
    resultDiv.style.display = "block";


        }
    </script>
