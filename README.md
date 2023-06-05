Задача 1: Скрабл
В настольной игре Скрабл (Scrabble) каждая буква имеет определенную ценность. В случае с английским алфавитом очки распределяются так:

A, E, I, O, U, L, N, S, T, R – 1 очко;
D, G – 2 очка;
B, C, M, P – 3 очка;
F, H, V, W, Y – 4 очка;
K – 5 очков;
J, X – 8 очков;
Q, Z – 10 очков.
А русские буквы оцениваются так:

А, В, Е, И, Н, О, Р, С, Т – 1 очко;
Д, К, Л, М, П, У – 2 очка;
Б, Г, Ё, Ь, Я – 3 очка;
Й, Ы – 4 очка;
Ж, З, Х, Ц, Ч – 5 очков;
Ш, Э, Ю – 8 очков;
Ф, Щ, Ъ – 10 очков.
Напишите программу, которая вычисляет стоимость введенного пользователем слова. Будем считать, что на вход подается только одно слово, которое содержит либо только английские, либо только русские буквы.



import re
def isCyrillic(text):
	return bool(re.search('[а-яА-Я]', text))
points_en = {1:'AEIOULNSTR',
      	2:'DG',
      	3:'BCMP',
      	4:'FHVWY',
      	5:'K',
      	8:'JZ',
      	10:'QZ'}
points_ru = {1:'АВЕИНОРСТ',
      	2:'ДКЛМПУ',
      	3:'БГЁЬЯ',
      	4:'ЙЫ',
      	5:'ЖЗХЦЧ',
      	8:'ШЭЮ',
      	10:'ФЩЪ'}
text = input().upper()
if isCyrillic(text):
	print(sum([k for i in text for k, v in points_ru.items() if i in v]))
else:
	print(sum([k for i in text for k, v in points_en.items() if i in v]))
  
  
  
  Задача 2: Рюкзак
Турист собирается в поход. Он сможет нести N кг вещей. Но вещей, которые он запланировал уложить в рюкзак, оказалось намного больше. Нужно определить, какие вещи от наиболее тяжелых к самым легким поместятся в рюкзак.


things = {'зажигалка': 20, 'компас': 100, 'фрукты': 500, 'рубашка': 300,
      	'термос': 1000, 'аптечка': 200, 'куртка': 600, 'бинокль': 400, 'удочка': 1200,
          'салфетки': 40, 'бутерброды': 820, 'палатка': 5500, 'спальный мешок': 2250, 'жвачка': 10}
ves = int(input()) * 1000
sorted_things = dict(sorted(things.items(), key=lambda x: -x[1]))
for k, v in sorted_things.items():
	if v <=  ves:
    	print(k, sep='/n')
    	ves -= v
      
Задача 3. Email-адреса
Данные об email-адресах студентов хранятся в словаре:

emails = {'mgu.edu': ['andrei_serov', 'alexander_pushkin', 'elena_belova', 'kirill_stepanov'],
      	'gmail.com': ['alena.semyonova', 'ivan.polekhin', 'marina_abrabova'],
      	'msu.edu': ['sergei.zharkov', 'julia_lyubimova', 'vitaliy.smirnoff'],
      	'yandex.ru': ['ekaterina_ivanova', 'glebova_nastya'],
      	'harvard.edu': ['john.doe', 'mark.zuckerberg', 'helen_hunt'],
      	'mail.ru': ['roman.kolosov', 'ilya_gromov', 'masha.yashkina']}
        
        
        print(*sorted({i + '@' + k for k, v in emails.items() for i in v}), sep = '\n')
        
  Задача 4: Права доступа
Вирус повредил систему прав доступа к файлам. Известно, что над каждым файлом можно производить определенные действия:

запись – W;
чтение – R;
запуск – X.
На вход программе подается:

число n – количество файлов;
n строк с именами файлов и допустимыми операциями;
число m – количество запросов к файлам;
m запросов вида «операция файл».
Для каждого допустимого запроса программа должна возвращать OK, для недопустимого – Access denied.



names = {}
rights = {'W': 'write', 'R': 'read', 'X': 'execute'}
for i in range(int(input())):
	x = input().split()
	names[x[0]] = [rights[i] for i in x[1:]]
for i in range(int(input())):
	comm, n = input().split()
	print('OK' if comm in names[n] else 'Access denied')
  
  
  
  
 Задача 5: Продажи
Напишите программу, которая подсчитывает количество единиц товаров, приобретенных покупателями онлайн-магазина. На вход программе подается число n – количество записей о покупках, а затем n строк вида «Покупатель Товар Количество». Для каждого покупателя программа должна выводить список покупок.


sales = {}
for _ in range(int(input())):
	name, item, count = input().split()
	sales[name][item] = sales.setdefault(name, {}).setdefault(item, 0) + int(count)
for key in sorted(sales):
	print(f'{key}:')
	for i in sorted(sales[key].items()):
    	print(*i)
      
Задача 6: Объединение словарей
В Python предусмотрено объединение словарей:

merged_dict = {**dict1, **dict2}

Однако если в словарях есть одинаковые ключи, ключу в объединенном словаре будет присвоено значение из второго словаря. Напишите программу, которая объединяет два словаря и суммирует значения одинаковых ключей.

Решение:

Воспользуемся методом get() , который принимает второй аргумент – значение по умолчанию, в нашем случае это должен быть 0. Кроме того, применим объединение множеств с помощью оператора |:

        
dict1 = {'яблоки': 100, 'бананы': 333, 'груши': 200,
         'апельсины': 300, 'ананасы': 45, 'лимоны': 98,
     	'сливы': 76, 'манго': 34, 'виноград': 90, 'лаймы': 230}
dict2 = {'яблоки': 300, 'груши': 200, 'бананы': 400,
     	'малина': 777, 'ананасы': 12, 'лаймы': 123, 'черника': 111, 'арбузы': 666}
merged_dict = {key: dict1.get(key, 0) + dict2.get(key, 0) for key in set(dict1) | set(dict2)}
print("Объединенный словарь:", merged_dict)


Задача 8: Редкое слово
Напишите программу, которая принимает на вход строку, и выводит слово, которое встречается во фразе реже всего. Если редких слов несколько, нужно вывести то, которое меньше в лексикографическом порядке. Регистр слов не учитывается, знаки препинания в предложениях игнорируются.


Решение:

Для подсчета символов, слов и т. п. удобно использовать метод get(), а для сортировки – лямбда-функцию, которая обеспечит вывод наименьшего из редких слов:

        
words = {}
for i in input().split():
	i = i.strip('.,!?:;-').lower()
	words[i] = words.get(i, 0) + 1 
print(min(words.items(), key=lambda x: (x[1], x[0]))[0])
      
      using System;
using System.Collections.Generic;

class Program
{
    static void Main(string[] args)
    {
        Dictionary<int, string> pointsEn = new Dictionary<int, string>()
        {
            { 1, "AEIOULNSTR" },
            { 2, "DG" },
            { 3, "BCMP" },
            { 4, "FHVWY" },
            { 5, "K" },
            { 8, "JX" },
            { 10, "QZ" }
        };

        Dictionary<int, string> pointsRu = new Dictionary<int, string>()
        {
            { 1, "АВЕИНОРСТ" },
            { 2, "ДКЛМПУ" },
            { 3, "БГЁЬЯ" },
            { 4, "ЙЫ" },
            { 5, "ЖЗХЦЧ" },
            { 8, "ШЭЮ" },
            { 10, "ФЩЪ" }
        };

        string text = Console.ReadLine().ToUpper();
        bool isCyrillic = ContainsCyrillic(text);

        int totalPoints = 0;
        if (isCyrillic)
        {
            totalPoints = CalculatePoints(text, pointsRu);
        }
        else
        {
            totalPoints = CalculatePoints(text, pointsEn);
        }

        Console.WriteLine(totalPoints);
    }

    static bool ContainsCyrillic(string text)
    {
        foreach (char c in text)
        {
            if (char.GetUnicodeCategory(c) == System.Globalization.UnicodeCategory.LowercaseLetter ||
                char.GetUnicodeCategory(c) == System.Globalization.UnicodeCategory.UppercaseLetter)
            {
                if (c >= 'А' && c <= 'я')
                {
                    return true;
                }
            }
        }
        return false;
    }

    static int CalculatePoints(string word, Dictionary<int, string> points)
    {
        int totalPoints = 0;
        foreach (char c in word)
        {
            foreach (var kvp in points)
            {
                if (kvp.Value.Contains(c))
                {
                    totalPoints += kvp.Key;
                    break;
                }
            }
        }
        return totalPoints;
    }
}


using System;
using System.Collections.Generic;
using System.Linq;

class Program
{
    static void Main(string[] args)
    {
        Dictionary<string, int> things = new Dictionary<string, int>()
        {
            { "зажигалка", 20 },
            { "компас", 100 },
            { "фрукты", 500 },
            { "рубашка", 300 },
            { "термос", 1000 },
            { "аптечка", 200 },
            { "куртка", 600 },
            { "бинокль", 400 },
            { "удочка", 1200 },
            { "салфетки", 40 },
            { "бутерброды", 820 },
            { "палатка", 5500 },
            { "спальный мешок", 2250 },
            { "жвачка", 10 }
        };

        int ves = int.Parse(Console.ReadLine()) * 1000;
        var sortedThings = things.OrderByDescending(x => x.Value);

        foreach (var kvp in sortedThings)
        {
            if (kvp.Value <= ves)
            {
                Console.WriteLine(kvp.Key);
                ves -= kvp.Value;
            }
        }
    }
}
using System;
using System.Collections.Generic;
using System.Linq;

class Program
{
    static void Main(string[] args)
    {
        Dictionary<string, List<string>> emails = new Dictionary<string, List<string>>()
        {
            { "mgu.edu", new List<string> { "andrei_serov", "alexander_pushkin", "elena_belova", "kirill_stepanov" } },
            { "gmail.com", new List<string> { "alena.semyonova", "ivan.polekhin", "marina_abrabova" } },
            { "msu.edu", new List<string> { "sergei.zharkov", "julia_lyubimova", "vitaliy.smirnoff" } },
            { "yandex.ru", new List<string> { "ekaterina_ivanova", "glebova_nastya" } },
            { "harvard.edu", new List<string> { "john.doe", "mark.zuckerberg", "helen_hunt" } },
            { "mail.ru", new List<string> { "roman.kolosov", "ilya_gromov", "masha.yashkina" } }
        };

        var sortedEmails = emails.SelectMany(kvp => kvp.Value.Select(email => email + "@" + kvp.Key)).OrderBy(email => email);

        foreach (string email in sortedEmails)
        {
            Console.WriteLine(email);
        }
    }
}
using System;
using System.Collections.Generic;

class Program
{
    static void Main(string[] args)
    {
        Dictionary<string, List<string>> names = new Dictionary<string, List<string>>();
        Dictionary<string, string> rights = new Dictionary<string, string>()
        {
            { "W", "write" },
            { "R", "read" },
            { "X", "execute" }
        };

        int n = int.Parse(Console.ReadLine());
        for (int i = 0; i < n; i++)
        {
            string[] input = Console.ReadLine().Split();
            string fileName = input[0];
            List<string> fileRights = new List<string>(input[1..]);

            names[fileName] = fileRights;
        }

        int m = int.Parse(Console.ReadLine());
        for (int i = 0; i < m; i++)
        {
            string[] input = Console.ReadLine().Split();
            string command = input[0];
            string fileName = input[1];

            if (names.ContainsKey(fileName) && names[fileName].Contains(command))
            {
                Console.WriteLine("OK");
            }
            else
            {
                Console.WriteLine("Access denied");
            }
        }
    }
}
using System;
using System.Collections.Generic;

class Program
{
    static void Main(string[] args)
    {
        Dictionary<string, Dictionary<string, int>> sales = new Dictionary<string, Dictionary<string, int>>();

        int n = int.Parse(Console.ReadLine());
        for (int i = 0; i < n; i++)
        {
            string[] input = Console.ReadLine().Split();
            string name = input[0];
            string item = input[1];
            int count = int.Parse(input[2]);

            if (!sales.ContainsKey(name))
            {
                sales[name] = new Dictionary<string, int>();
            }

            if (sales[name].ContainsKey(item))
            {
                sales[name][item] += count;
            }
            else
            {
                sales[name][item] = count;
            }
        }

        foreach (KeyValuePair<string, Dictionary<string, int>> kvp in sales)
        {
            Console.WriteLine($"{kvp.Key}:");
            foreach (KeyValuePair<string, int> item in kvp.Value.OrderBy(x => x.Key))
            {
                Console.WriteLine($"{item.Key} {item.Value}");
            }
        }
    }
}
using System;
using System.Collections.Generic;

class Program
{
    static void Main(string[] args)
    {
        Dictionary<string, int> dict1 = new Dictionary<string, int>()
        {
            { "яблоки", 100 },
            { "бананы", 333 },
            { "груши", 200 },
            { "апельсины", 300 },
            { "ананасы", 45 },
            { "лимоны", 98 },
            { "сливы", 76 },
            { "манго", 34 },
            { "виноград", 90 },
            { "лаймы", 230 }
        };

        Dictionary<string, int> dict2 = new Dictionary<string, int>()
        {
            { "яблоки", 300 },
            { "груши", 200 },
            { "бананы", 400 },
            { "малина", 777 },
            { "ананасы", 12 },
            { "лаймы", 123 },
            { "черника", 111 },
            { "арбузы", 666 }
        };

        Dictionary<string, int> mergedDict = new Dictionary<string, int>();

        foreach (KeyValuePair<string, int> kvp in dict1)
        {
            mergedDict[kvp.Key] = kvp.Value;
        }

        foreach (KeyValuePair<string, int> kvp in dict2)
        {
            if (mergedDict.ContainsKey(kvp.Key))
            {
                mergedDict[kvp.Key] += kvp.Value;
            }
            else
            {
                mergedDict[kvp.Key] = kvp.Value;
            }
        }

        Console.WriteLine("Объединенный словарь:");
        foreach (KeyValuePair<string, int> kvp in mergedDict)
        {
            Console.WriteLine($"{kvp.Key}: {kvp.Value}");
        }
    }
}
using System;
using System.Collections.Generic;
using System.Linq;

class Program
{
    static void Main(string[] args)
    {
        Dictionary<string, int> words = new Dictionary<string, int>();
        string[] inputWords = Console.ReadLine().Split();

        foreach (string word in inputWords)
        {
            string processedWord = word.TrimEnd('.', ',', '!', '?', ':', ';').ToLower();

            if (!string.IsNullOrEmpty(processedWord))
            {
                if (words.ContainsKey(processedWord))
                {
                    words[processedWord]++;
                }
                else
                {
                    words[processedWord] = 1;
                }
            }
        }

        KeyValuePair<string, int> rarestWord = words.OrderBy(x => x.Key).ThenBy(x => x.Value).First();
        Console.WriteLine(rarestWord.Key);
    }
}

      
