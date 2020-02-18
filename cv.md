1. Matvei Armanov
2. cell phone: +79634727966, e-mail: fftramza@yandex.ru
3. Used to be a research associate in the field of technical physics. I want to become a skillful web-developer and get opportunity to work on a large project.
4. MatLab, Python
5. A python-script that conducting a comparison between pairs of Moscow universities wiki-pages' lists of internal wiki-links and making a table with number of matches.

from urllib.request import urlopen
from bs4 import BeautifulSoup


def getlinks(url):
    response = urlopen('https://en.wikipedia.org' + url)
    html = response.read().decode('utf8')
    soup = BeautifulSoup(html)
    links = set()
    for link in soup.find_all('a'):
        if link.has_attr('href'):
            s = link.get('href')
            if (s.startswith('/wiki/') or s.startswith('/w/')) and ':' not in s:
                links.add(s)
    return links

allunivs = list(getlinks('/wiki/Category:Universities_in_Moscow'))
allunivs = sorted(allunivs)
linkunivs = {}
for univ in allunivs:
    linkunivs[univ] = getlinks(univ)

fout = open('table.html', 'w', encoding='utf8')
print('''<html>
            <body>
                <table>
                    <tr>''', file=fout)
UnivsReduced = []
for univ in sorted(allunivs):
    UnivsReduced.append(univ[6:].replace('_', ' '))

print('<td></td><td>', '</td><td>'.join(UnivsReduced), '</tr>', file=fout)
for univ1 in sorted(allunivs):
    print('<tr><td>', univ1[6:].replace('_', ' '), '</td>', file=fout)
    for univ2 in sorted(allunivs):
        print('<td>', len(linkunivs[univ1] & linkunivs[univ2]), '</td>', file=fout)
    print('</tr>', file=fout)
print('''</table>
    </body>
</html>''', file=fout)
fout.close()

6. Not much experience in web-development.
7. I have graduated from National Research Nuclear University in 2012. My major was solid state physics. I'm training on HTMLacademy, Codewars, w3schools.com.
8. I've translated dozens of scientific papers from english to russian.