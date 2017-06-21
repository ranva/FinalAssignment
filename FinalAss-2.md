
# Final Assignment
## In this part of the assignment we downloaded data from 3 different sources. Wikipedia, Cnn-economy, and Nbc. we analyzed the data to and understand what can help us
## Function to convert a raw review to a string of words The input is a single string , and  the output is a single string 
### the function will clean the data and convert the data to meaningful data. it will remove non-letters, remove unwanted chaaracters, convert the stinrg to lower case and will remove stop words

## Stemming
### stemming is the process of reducing inflected (or sometimes derived) words to their word stem, base or root form. Porter Stemming and Lemmatizing (both available in NLTK) would allow us to treat "messages", "message", and "messaging" as the same word, which could certainly be useful.


```python
# Import BeautifulSoup into your workspace
import re
import nltk
from bs4 import BeautifulSoup 
from nltk.corpus import stopwords # Import the stop word list
def review_to_words( raw_review ): 
    soup_article = BeautifulSoup(raw_review, "html.parser") 
 
    # Use regular expressions to do a find-and-replace
    cleanedSoup_article = re.sub("[^a-zA-Z]",   # The pattern to search for: in this case- all characters but english letters
                          " ",                   # The pattern to replace it with
                          soup_article.get_text() )  # The text to search
   
    lower_case = cleanedSoup_article.lower() # Convert to lower case 
    words = nltk.word_tokenize(lower_case) # Split into words
    words = [w for w in words if not w in stopwords.words("english")]
    porter = nltk.PorterStemmer()
    lancaster = nltk.LancasterStemmer()
    [porter.stem(w) for w in words]
    return ( " ".join( words ))
```


## Get 50 random articles from wikipedia 
## Analyze the data
## Most of the code is not active because the services is not permitted more then once for day. as a result we save the data in pickle file and read it each time 


```python
import wikipedia
import pickle
import unicodedata


#wikipedia.set_lang("en")
#test = wikipedia.random(1)
#wikipedia.page(test).summary

#def random_page():
#    random = wikipedia.random(1)
#    try:
#        result = wikipedia.page(random).summary
#    except wikipedia.exceptions.DisambiguationError as e:
#        result = random_page()
#    return result
#counter = 1
#articles = []

#while counter < 51:
#    a = random_page()
#    print(a)
#    print("*****************")
#    a = unicodedata.normalize('NFKD', a).encode('ascii','ignore')
#    articles.append(a)
#    counter = counter + 1
    
#print counter
#cnn_paper = newspaper.build('http://cnn.com')
#for article in cnn_paper.articles:
#print(len(articles))







```


```python
print(len(articles))
```

    50



```python
print articles
```

    ['"Love Song" is M-Flo\'s twenty-second single under Rhythm Zone. It contains 2 new songs for their next 2007 album, Cosmicolor, a remix of "Lotta Love", and instrumentals. It was released on November 8, 2006. First pressings of the single will include CD-Extra footage of a live "Summer Time Love" performance.\n"Love Song" is Bonnie Pink\'s twenty-sixth single.', 'The 197172 season was the 92nd season of competitive football by Rangers.', 'Afromarengo plana is a jumping spider species of the genus Afromarengo that lives in South Africa.', 'Grisana is a genus of moths of the Noctuidae family.', 'Kshatriya Kulavatauns is a title of nobility, which was conferred upon the seventeenth century Indian warrior king, Chhatrapati Shivaji Raje Bhosale and it means the head or chief of Kshatriya race. Kshatriya is one of the four varnas of Hinduism and kulavantas means the head of the kula or race. The title continues to be used by Shivajis descendants.', 'The Robert Sands Estate was a historic home located at Rhinebeck, Dutchess County, New York. The house was built about 1796 and is a  2 12-story, brick filled wood frame building, with a gable roof and sheathed in clapboard. It sat on an extant stone foundation and measured five bays wide by four deep. Also on the property were a contributing  1 12-story frame cottage and four frame farm outbuildings, including a Dutch barn.\nIt was added to the National Register of Historic Places in 1987. In 2015 the National Park Service, which oversees the Register, announced that it was considering a request to remove it as a result of a 1999 fire that left only the foundation. It did so in August of that year.>', "Cowboy Ninja Viking is an Image Comics comic book created by writer A.J. Lieberman and artist Riley Rossmo. The series debuted in 2009, released through Image Comics' partner studio Shadowline.", 'Das Kriminalmuseum was a German television series. It ran from 1963 to 1970 on ZDF and was one of its first programs. Each episode began with a tracking shot through an unspecified crime museum, stopping at one of the displays, whose story was then told. Each episode was between 60 and 75 minutes long and featured different actors as the criminal commissioner. The best known was Erik Ode, who in 1969 moved to Der Kommissar, appearing in 97 episodes. The theme music of the series was written by German composer Martin Bottcher, who also composed the complete scores for five episodes.', "Universal Music Latin Entertainment, a division of Universal Music Group (Vivendi), is a record company specialized in producing and distributing Latin Music in Mexico, United States and Puerto Rico. UMLE includes famous Latin music labels such as Universal Music Latino, Fonovisa Records, Universal Music Mexico, Capitol Latin, Machete Music and Disa Records.\nThe record company was created in 2008 with the acquisition of Univision Music Group and combining it with Universal's top Latin artists, along with much of the Latin back catalog of UMG.", 'Molineux Stadium (/mlnju/ MOL-i-new) is a Championship football stadium situated in Wolverhampton, England. It has been the home ground of Wolverhampton Wanderers Football Club since 1889, and has a long history as the first stadium ever built for the Football League, one of the first grounds in the country to install floodlights, as well as hosting some of the first European club games in the 1950s.\nAt the time of its multimillion-pound renovation in the early 1990s, Molineux was one of the biggest and most modern stadia in England, though it has since been eclipsed by many other ground developments. The stadium has however hosted England internationals and, more recently, England under-21 internationals, as well as the first UEFA Cup Final in 1972. Although currently a 31,000 seater stadium, the record attendance at Molineux stands at 61,315.\nInitial plans were announced in May 2010 to rebuild two sides of the stadium by the 201415 season to increase capacity to around 36,000. The first stage of this project began in summer 2011 and was completed on course for the start of the 201213 season. There are also provisional future plans for a longer term redevelopment of every stand that could potentially create a 50,000 capacity.\n\n', 'Americo Sebastiano Costantino (born October 1, 1961) is an Italian-American retired professional wrestler and wrestling manager. He performed under the ring names Rico Costantino and Rico in World Wrestling Entertainment (WWE) from 2001 to 2004. He is currently wrestling for the Future Stars of Wrestling promotion in Las Vegas, Nevada.', 'Lance Edward "Lem" Massey (September 20, 1909  June 4, 1942) He was a native of Syracuse, New York and was the only child of Walter Griffith Massey and Florence Lance Massey. Growing up in Watertown, New York, he attended two years of high school in Watertown, and then entered the Severn School located in Severna Park, Maryland in 1925. After graduating from Severn in 1926, he was accepted into the U.S. Naval Academy when he was sixteen\nAfter graduating from the Naval Academy in 1930, he was given his commission as an Ensign, and he was ordered to the battleship USS Texas (BB-35). After serving for a year aboard the USS Texas he entered flight training in Pensacola Naval Air Station in 1931 and won his Naval Aviator wings in January 1932. He was assigned to Scouting Squadron 3 aboard the aircraft carrier USS Lexington (CV-2) for the next three years and as ships company on the USS Lexington. He subsequently served a two-year tour in Pensacola Naval Air Station in Florida as a Flight Instructor. While at Pensacola he was married to Marjorie Drake Kelsey, the widow of Lieutenant (j.g.) James Kelsey, a 1931 graduate of the US Naval Academy. In June 1937 Lieutenant t(jg) Massey reported to Observation Squadron 3 aboard the battleship USS New Mexico (BB-40) whose home port was Long Beach, California. In August 1937, he was promoted to the rank of Lieutenant. In January 1940, Observation Squadron Three was transferred to the USS Idaho (BB-42) where he stayed until July 1940 when he was sent to Naval Air Station, Pensacola. In October 1941 he was reassigned to the USS Enterprise (CV-6) as the Executive Officer of Torpedo Squadron Six and when the United States was attacked by Japan in December 1941, he was serving in this capacity\nHe was promoted to the rank of Lieutenant Commander in January 1942. He was active in several major actions during the first seven months of 1942. On February 1, 1942, his squadron, Torpedo Squadron Six, consisting of nine TBD-1 Devastator torpedo planes, made the first airborne torpedo attack in U.S. Naval history. For this attack against Japanese shipping at Kwajalein Atoll, in the Marshall Islands, in which he sank an 18,00 ton Japanese transport, the Bordeaux Maru, he was awarded the Distinguished Flying Cross. The following month aboard the USS Enterprise and its air wing escorted the USS Hornet (CV-8) as it carried General Jimmy Doolittles renowned Tokyo Raiders as they attacked mainland Japan.', 'Neaspilota is a genus of tephritid or fruit flies in the family Tephritidae.', 'The Faulknor family was an English family from Northamptonshire, of which several generations served as officers in the Royal Navy.', 'Stefan Dimle (born 7 June 1967 in Koping, Sweden) is the bassplayer in the progressive band Morte Macabre and he is a former member of Landberk and Paatos. He is the driving force in the company Mellotronen who also is the organiser of the floating rock festival named the Melloboat which are held aboard the ship Galaxy. Mellotronen runs the community Mello-Club at a cafe in Stockholm.\nDuring the 1980s was Stefan Dimle member of several local rock bands in his former hometown Borlange. One of the bands was Kajuku. Some members from that band are currently in Opeth and Anekdoten. 1986 did Stefan Dimle start the rock club Mellotronen in Borlange. The company existed on a parallel basis in Stockholm and Borlange. The shop had a huge section of rare and hard to find CDs & LPs in the field of progressive rock . Mellotronen became an important headquarters for musicians and fans of progressive rock during the 1990s. The shop Mellotronen where located on the fashionable street Kakbrinken in Gamla Stan in the center of Stockholm. Nowadays one can find Dimle and his company in the city of Gustavsberg.\nStefan Dimle was a member of the band Landberk between 1990-1997. They recorded three albums and two EPs on various record labels like Record Heaven, Mega Rock and the American label Laser\'s Edge. The progressive rock groups Landberk, Anglagard and Anekdoten co-operated a lot, and all three of them used the instrument Mellotron as a main instrument. These three groups led the way for many new bands in the progressive genre. All three of them were famous on an international level.\nThe label Mellotronen started 1991 with a CD reissue of Solid Grounds debut album from 1976. Since then has Dimle released around 50 different CD and vinyl albums. The latest ones are a double-CD with Trettioariga Kriget and two albums with Sabu Martinez. Dimle and Mellotronen has co-operated a lot with labels like Universal, The National Swedish Radio, MNW, Sony and EMI.\nTogether with members from Landberk and Anekdoten, Dimle started the project Morte Macabre, who has made a career in film circuits with their repertoire of new versions of old soundtracks from mainly Italian horror movies. The band Paatos started in 1999 and Dimle performed with them til 2008. Paatos has released four albums and 7" inch vinyl single. Dimle has also performed with Emma Nordenstam, And the machine said behold, Turid and Onkel Kankel and his kankelbar.\nIn January 2007 organised Dimle a rock festival on board the ship Silja Festival to celebrate the 20th anniversary of the Mellotronen company. Among the many artists that performed on board can the following ones be mentioned, Flasket Brinner, November, Asoka, Morte Macabre, Solid Ground and Emma Nordenstam. In March 2008 was it time for a 2nd rock cruise on the ship Silja Symphony. Many people came to see bands like Opeth, Katatonia and Comus. In April 2009 the third rock cruise was supposed to take place with the destination Finland, this time on board the M/S Galaxy. However, a few months before the date Dimle announced that Melloboat 2009 had been cancelled. Among the many artist that was supposed to perform on the cruise was Meshuggah, May Blitz and Steven Wilson.', "Holzdorf is a village in the municipality of Jessen (Elster) in the district of Wittenberg in the German state of Saxony-Anhalt. It has about 1,400 inhabitants. Previously a separate municipality in the district of Kremitz, it became part of the amalgamated municipality of Jessen on 1 March 2004.\nHolzdorf, with various shops and doctors' offices, is a regional center for the surrounding villages. In addition to farming, the nearby Schonewalde/Holzdorf Air Base with about 400 staff, is the main source of income of the residents. The air base itself is within the city Schonewalde in Brandenburg.", 'Tredinnick is a Cornish surname. It derives from one of the places called Tredinnick; Tredinnick is formed from the elements "tre-" (homestead) and either "dynek" (fortified), "eythynek" (overgrown with gorse) or "redynek" (overgrown with bracken).\nNotable people with the surname include:\nDavid Tredinnick (actor), Australian actor\nDavid Tredinnick (politician) (born 1950), British politician\nMark Tredinnick (born 1962), Australian poet and writer\nMiles Tredinnick (born 1955), English musician, and stage and screen writer\nNoel Tredinnick (born 1949), English organist and composer', "The 189798 Scottish Cup was the 25th season of Scotland's most prestigious football knockout competition. The Cup was won by Rangers when they beat Kilmarnock 2-0 in the final.", 'Gunther Schmidt (*1939 in Rudersdorf near Berlin) is a German mathematician who works also in informatics.', 'Robert S. Sargent (19122006) was an electrical engineer, Defense Department defensive weapons specialist, and published poet who lived most of his adult life in Washington, DC.', 'Broken Rites, or formally Broken Rites (Australia) Collective Inc., is an Australian non-profit organisation that is dedicated to exposing and denouncing cases in the Catholic sexual abuse scandal.', '"Deep Six" is a song by American rock band Marilyn Manson. The song was released to digital outlets on December 16, 2014 as the second single from the band\'s ninth studio album, The Pale Emperor (2015). A music video directed by Bart Hess was released on YouTube. The song was a hit on American Active Rock radio, peaking at number eight on Billboard\'s Mainstream Rock, becoming the band\'s highest peaking single ever on that chart.\n\n', 'USA-177, also known as GPS IIR-11 and GPS SVN-59, is an American navigation satellite which forms part of the Global Positioning System. It was the eleventh Block IIR GPS satellite to be launched, out of thirteen in the original configuration, and twenty one overall. It was built by Lockheed Martin, using the AS-4000 satellite bus.\nUSA-177 was launched at 17:53:00 UTC on 20 March 2004, atop a Delta II carrier rocket, flight number D303, flying in the 7925-9.5 configuration. The launch took place from Space Launch Complex 17B at the Cape Canaveral Air Force Station, and placed USA-177 into a transfer orbit. The satellite raised itself into medium Earth orbit using a Star-37FM apogee motor.\nBy 20 May 2004, USA-177 was in an orbit with a perigee of 20,095 kilometres (12,486 mi), an apogee of 20,271 kilometres (12,596 mi), a period of 718 minutes, and 55 degrees of inclination to the equator. It is used to broadcast the PRN 19 signal, and operates in slot 3 of plane C of the GPS constellation. The satellite has a mass of 2,032 kilograms (4,480 lb), and a design life of 10 years. As of 2012 it remains in service.', 'Luan County station (Chinese: ) is a Chinese railway station located in Luan County, on the Jingha Railway.', 'Stanek [stank] is a village in the administrative district of Gmina Michaowo, within Biaystok County, Podlaskie Voivodeship, in north-eastern Poland, close to the border with Belarus. It lies approximately 11 kilometres (7 mi) north-west of Michaowo and 23 km (14 mi) east of the regional capital Biaystok.', 'Carlo Pezzati (October 28, 18921944) was an Italian politician, the mayor of the Italian city of Piacenza.\nCarlo was born to Pio and Defina Elmonti Pezzati in the village of Torre Gandini, outside Piacenza, in 1892. He would eventually become the mayor of Piacenza.\nIn 1944 he was killed by the partisans. He was laid to rest in the cemetery of Torre Gandini.', 'John William Moore (June 9, 1877  December 11, 1941) was a U.S. Representative from Kentucky.\nBorn in Morgantown, Kentucky, Moore attended the public schools and completed a commercial course at Bryant and Stratton College at Louisville in 1897. He became a clerk with the Morgantown Deposit Bank in 1898. He engaged in the timber business 1899-1919. Cashier for the Morgantown Deposit Bank 1920-1925.\nMoore was elected as a Democrat to the Sixty-ninth Congress in a special election, to fill the vacancy caused by the death of United States Representative Robert Y. Thomas, Jr. and reelected to the succeeding Congress (December 26, 1925  March 3, 1929). He was an unsuccessful candidate for reelection to the Seventy-first Congress in 1928.\nMoore was elected as a Democrat to the Seventy-first Congress in a special election, to fill the vacancy caused by the death of United States Representative Charles W. Roark, and reelected to the succeeding Congress (June 1, 1929  March 3, 1933). He was not a candidate for renomination to the Seventy-third Congress in 1932. He resumed his former business pursuits. He was employed in the Federal Housing Administration at Washington, D.C., as an assistant comptroller 1935-1941. He died in Washington, D.C., December 11, 1941. He was interred in Morgantown Cemetery, Morgantown, Kentucky.', 'The 26th Division (Spanish: 26a Division) was a division of the Spanish Republican Army in the Spanish Civil War. It was formed in April 1937 in Aragon from the militarized Columna Durruti during the reorganization of the Spanish Republican Armed Forces.\nThe 26th Division included the 119th, 120th and 121st mixed brigades throughout the Civil War. It fought in the Huesca Offensive, the Battle of Belchite, the Aragon Offensive and the Battle of the Segre. Finally it was disbanded in February 1939 after the withdrawal and rush to the border that followed the rebel Catalonia Offensive.', 'The Pelham Range is a small mountain range on southern Vancouver Island, British Columbia, Canada, located northeast of Sarita and between the Sarita River and Alberni Inlet. It has an area of 52 km2 and is a subrange of the Vancouver Island Ranges which in turn form part of the Insular Mountains.', 'Katzenthal is a commune in the Haut-Rhin department in Grand Est in north-eastern France.', 'Psyrassa sallaei is a species of beetle in the family Cerambycidae.', 'Juan Manuel Coello Torres (born 21 May 1976) is a retired Honduran association footballer.\nHe currently is coach of the Motagua reserves team.', 'Holy Trinity Church is a Church of Scotland parish church in St Andrews, Fife. It is a Category A listed building.', 'Athyma glora is a species of nymphalid butterfly.', "Amanda Nicole Poach (born July 25, 1987) is an American soccer player from Bowie, Maryland.\nPoach represented the United States at the 2006 FIFA U-20 Women's World Championship where the team finished in fourth place.", 'The Lone Shark was a weekly, 30-minute public-access television cable TV program which broadcast for ten years (19912001) on WFAC-TV (19912000) and SoundView Community Television (20002001). Both television stations were part of Cablevision of Southern Connecticuts cable system, which spans the southwestern coast of Connecticut from the New York State border to the middle of New Haven County.\nThe Lone Shark was hosted by the program\'s creator and Executive Producer Jim Sharky and co-hosted by the program\'s Producer Sean Haffner (a.k.a. Sean The Producer). Although the program was unscripted, Sharky would usually have a list of topics that he wanted to discuss with Haffner on each episode. The Lone Shark was known for its fast pace, strong language and adult themes, often pushing the limits of what station managers believed could be allowed on television.\nThe Lone Shark was originally recorded in-studio or on-location and edited before broadcast, but after 1993 the program was broadcast "live" without a broadcast delay, editing or censor. In August 2001 the program was permanently suspended from production by the SoundView Television station management after The Lone Shark aired three seconds of a graphic adult sex video on live television during prime time.', 'Peppy (from peppermint) is the polar bear mascot and icon of Fox\'s Glacier Mints, a brand of boiled mint manufactured by Fox\'s Confectionery in the United Kingdom. Peppy was introduced to confectionery packaging in 1922. At around the same time, Fox\'s commissioned a taxidermist to shoot and stuff a real polar bear, which was put out on display at such public events as football matches and carnivals to advertise the Glacier Mints. The exhibition was taken all over the country, and eventually incorporated as many as four other stuffed polar bears. In the 1960s, after the advent of televised advertising and after Rowntrees acquired the company, the exhibition was deemed politically incorrect and was removed from public circulation. Television commercials which featured Peppy were later produced.\nIn 2003, the original Peppy  measuring 1.5 m (4 ft 11 in) high and 2 m (6 ft 7 in) long, and with an indeterminate gender  was donated to the New Walk Museum in Leicester, the city in which Fox\'s Confectionery is based. The stuffed bear had been lost in a company factory for approximately 20 years. A brand manager said of the donation, "We found it in the back when we were clearing out and decided to donate it to a museum - the best place for it. We didn\'t want it in the reception because it\'s so gory we feared it could scare the customers when they visited." After the acquisition, the museum commenced a restoration process which took six years to complete. Peppy was displayed in a public exhibition at the museum from 24 January to 5 April 2009.', "Earl Thomas Ferrell (born March 27, 1958 in Halifax, Virginia), is a former professional American football player who was selected by the St. Louis Cardinals in the 5th round of the 1982 NFL Draft. A 6 ft 0 in (1.83 m), 220 lbs. running back from East Tennessee State, Ferrell played his entire NFL career for the Cardinals from 1982 to 1989. He led all Cardinals running backs in rushing yards during the 1988 and 1989 seasons, the team's first two years playing in Phoenix.\nHe was the second player, and one of only four in the school's history, to be selected in the draft and play in the NFL after playing college football at ETSU.\nDespite a Pro Bowl appearance in each of his final two seasons, Ferrell's career was cut short due to problems with illegal drugs. In 1988, Ferrell reportedly tested positive three times for cocaine, and prior to the 1990 season, he was suspended for one year due to another failed drug test. He never played in the NFL again. On getting the news of his suspension, Ferrell chose to retire.", 'Where the Happy People Go is the third studio album by American soul-disco group, The Trammps, released in 1976 through Atlantic Records.', 'Decellularization of porcine heart valves is the removal of cells along with antigenic cellular elements  by either physical or chemical decellularization of the tissue. This decellularized valve tissue provides a scaffold with the remaining extracellular matrix (ECM) that can then be used for tissue engineering and valve replacement in humans inflicted with valvular disease. Decellularized biological valves have potential benefit over conventional valves through decreased calcification which is thought to be an immuno-inflammatory response initiated by the recipient.', "Charley's Aunt is a farce in three acts written by Brandon Thomas. It broke all historic records for plays of any kind, with an original London run of 1,466 performances.\nThe play was first performed at the Theatre Royal, Bury St Edmunds in February 1892. It was produced by former D'Oyly Carte Opera Company actor W. S. Penley, a friend of Thomas, who appeared in the principal role of Lord Fancourt Babberley, an undergraduate whose friends Jack and Charley persuade him to impersonate the latter's aunt. The piece was a success, and it then opened in London at the Royalty Theatre on 21 December 1892 and quickly transferred to the larger Globe Theatre on 30 January 1893 to complete its record-breaking run.\nThe play was a success on Broadway in 1893, where it had another long run. It also toured internationally and has been revived continually and adapted for films and musicals.", 'Francois Lesieur Desaulniers (1785  August 7, 1870) was a Quebec farmer and political figure.\nHe was born in Yamachiche in 1785. He served as lieutenant-colonel in the local militia. In 1805, he married Charlotte, the daughter of Augustin Rivard, who represented Saint-Maurice in the legislative assembly from 1792 to 1796. Desaulniers was elected to the Legislative Assembly of Lower Canada for Saint-Maurice in an 1836 by-election as a member of the parti patriote. He was elected to the Legislative Assembly of the Province of Canada for the same region in 1844.\nHe died at Yamachiche in 1870.\nHis son Louis-Leon was a member of the Canadian House of Commons.', 'The choanoderm is a type of cell layer composed of flagellated collar cells, or choanocytes found in sponges.', 'This article presents lists of the literary events and publications in 1925.', 'Sawoszewek [swavvk] is a village in the administrative district of Gmina Kleczew, within Konin County, Greater Poland Voivodeship, in west-central Poland. It lies approximately 2 kilometres (1 mi) north of Kleczew, 20 km (12 mi) north of Konin, and 87 km (54 mi) east of the regional capital Poznan.\nThe village has a population of 530.', 'Valdres videregaande skule is a high school located in the Valdres area of eastern Norway. The school is the primary high school for the vast majority of students in the greater Valdres area, and offers a relatively broad range of subjects.\nSince distances in the area are quite big, many students live in small apartments closer to the school (e.g. students from the areas farthest away may take up to an hour of travel every day by bus just to get to school).\nThe school was until 2001 split in two sections, one in Leira and another at Fagernes, but a new building and heavy investment from the municipal extended the Leira section to cover all the students.\nAt the time of writing, the principal is Kari Elisabeth Rustad, and the student count is generally around 500.', 'Nalkheda is a village in the Bhopal district of Madhya Pradesh, India. It is located in the Berasia tehsil.', 'The Puerto Rican Nationalist Party Revolts of the 1950s were a series of coordinated armed protests for the independence of Puerto Rico led by the president of the Puerto Rican Nationalist Party, Don Pedro Albizu Campos, against the United States Government rule on the Island. The Party repudiated the "Free Associated State" (Estado Libre Asociado) status that had been enacted in 1950 and which the Nationalists considered a continuation of colonialism.\nThe Party organized a series of uprisings to take place in various Puerto Rican cities on October 30, 1950. The uprisings were suppressed by strong ground and air military force under the command of Puerto Rico National Guard Major General Luis R. Esteves. In a related event, on November 1 of that year, two Nationalists from New York City attempted to storm the Blair House in a failed effort to assassinate U.S. President Harry S. Truman, who supported the Puerto Rican government effort to draft a constitution that would rename the local government as a commonwealth of the United States and provide some limited local autonomy.\nIn 1952, nearly 82% of Puerto Rican voters approved the Constitution of the Estado Libre Associado. But the Nationalists considered the outcome of the vote a political farce since the referendum offered no option to vote in favor of independence or statehood, restricting the choices to only two: a continuation of the colonial status existing at that time and the proposed new commonwealth status.\nOn March 1, 1954, in another armed assault, four Nationalists fired shots from the visitors\' gallery in the House of Representatives of the United States Capitol during a full floor debate, wounding five Congressmen, one seriously. The Nationalists were protesting what they perceived as a continuation of a colonial status in Puerto Rico.', '"Until It Sleeps" is a song by American heavy metal band Metallica from their 1996 album Load. It was the band\'s first number one song on the US Billboard Hot Mainstream Rock Tracks chart, as well as their first and only song as of the release of Death Magnetic to hit the top 10 of the Billboard Hot 100, debuting and peaking at number 10.', 'Rising Sun High School is a public high school in Rising Sun, Indiana. It is part of Rising Sun-Ohio County Community Schools and is the only high school in Ohio County.']


## Search for multiple values


```python
from collections import Counter
[k for k,v in Counter(articles).items() if v>1]
    
```




    []



## Get  50 articles from cnn economy


```python
import newspaper

#cnn_paper = newspaper.build('http://money.cnn.com/INTERNATIONAL/')
#bbc_paper = newspaper.build('http://www.bbc.com/news')
```

## Put the data of cnn into list


```python
#cnn_articles = []
#bbc_articles = []
c1 = 0

#for article in cnn_paper.articles:
#    if(c1 < 50): 
#        article.download()
#        article.parse()
#        article.nlp()
#        a = article.summary
#        a = unicodedata.normalize('NFKD', a).encode('ascii','ignore')
#        cnn_articles.append(a)
#        c1 = c1 + 1
    
print len(cnn_articles)
#print len(bbc_articles)
print c1




#for art in cnn_paper.articles:
#    cnn_articles.append(art.summary)
#print cnn_articles
```

    50
    0


## Get  50 articles from nbc


```python
#ny_paper = newspaper.build('http://www.nbcnews.com/')

```


```python
ny_paper_tech = []

c1 = 0

#for article in ny_paper.articles:
#    if(c1 < 50): 
#        article.download()
#        article.parse()
#        article.nlp()
#        a = article.summary
#        a = unicodedata.normalize('NFKD', a).encode('ascii','ignore')
#        ny_paper_tech.append(a)
#        c1 = c1 + 1
    
#print len(ny_paper_tech)
#print ny_paper_tech[0]
#print len(bbc_articles)
#print c1




#for art in cnn_paper.articles:
#    cnn_articles.append(art.summary)
#print cnn_articles
```

## Save the data in pickle file


```python
#print ny_paper_tech[10]
#data = articles + cnn_articles + ny_paper_tech

#with open('data.pickle', 'wb') as handle:
#    pickle.dump(data, handle, protocol=pickle.HIGHEST_PROTOCOL)

```


```python
with open('data.pickle', 'rb') as handle:
    data = pickle.load(handle)
len(data)

```




    150



## Call the review  function to clean the data


```python
c = 0
final_data = {'wiki' : [], 'cnn' : [], 'nbc' : []}
print len(data)
for d in data:
    review = review_to_words( d )
    if isinstance(review, unicode):
        a = unicodedata.normalize('NFKD', review).encode('ascii','ignore')
    if c < 50:
        final_data['wiki'].append(a)
      
    if c > 50 and c <= 100:
        final_data['cnn'].append(a)
      
    if c >= 100:
        final_data['nbc'].append(a)
    c = c + 1
    

print len(final_data)
print final_data['wiki'][2]
#review = review_to_words( data[3] )


```

    150
    3
    afromarengo plana jumping spider species genus afromarengo lives south africa


##  BOW - Bag of words The Bag of Words model learns a vocabulary from all of the documents, then models each document by counting the number of times each word appears.

### It helps us to understand better which data relates to which article


```python
print("Creating the bag of words...\n")
from sklearn.feature_extraction.text import CountVectorizer
def vectorize ( data_name ):
    # Initialize the "CountVectorizer" object, which is scikit-learn's
    # bag of words tool.  
    vectorizer = CountVectorizer(analyzer = "word",   \
                                 tokenizer = None,    \
                                 preprocessor = None, \
                                 stop_words = None,   \
                                 max_features = 50) 

    # fit_transform() Convert a collection of text documents (reviews in our example) to a matrix of token counts.
    # This implementation produces a sparse representation.
    # The input to fit_transform should be a list of strings.
    train_data_features = vectorizer.fit_transform(final_data[data_name])
#    train_data2 = vectorizer.fit_transform(final_data['cnn'])
#    train_data3 = vectorizer.fit_transform(final_data['nbc'])
    ###train_data_features = vectorizer.fit_transform(train['review'])

    # Numpy arrays are easy to work with, so convert the result to an 
    # array

    train_data_features = train_data_features.toarray()
    return ( train_data_features , vectorizer ) 
#    train_data2 = train_data2.toarray()
#    train_data3 = train_data3.toarray()
#    print(train_data_features.shape)
#    print(train_data2.shape)
#    print(train_data3.shape)
```

    Creating the bag of words...
    


## Print the features ( most common words ) 


```python
train_data_features_wiki , vec_wiki = vectorize( 'wiki' )
train_data_features_cnn , vec_cnn = vectorize( 'cnn' )
train_data_features_nbc , vec_nbc = vectorize( 'nbc' )
vocab_wiki = vec_wiki.get_feature_names()
vocab_cnn = vec_cnn.get_feature_names()
vocab_nbc = vec_nbc.get_feature_names()

print(vocab_wiki[0:50])
print(vocab_cnn[0:50])
print(vocab_nbc[0:50])
```

    [u'air', u'also', u'american', u'band', u'born', u'company', u'congress', u'county', u'december', u'dimle', u'first', u'football', u'four', u'high', u'january', u'latin', u'located', u'many', u'march', u'mellotronen', u'mi', u'music', u'naval', u'new', u'one', u'program', u'public', u'puerto', u'record', u'released', u'rico', u'rock', u'school', u'season', u'single', u'song', u'stadium', u'states', u'station', u'television', u'th', u'three', u'time', u'tredinnick', u'two', u'united', u'universal', u'uss', u'village', u'years']
    [u'air', u'airways', u'also', u'amazon', u'american', u'back', u'billion', u'boeing', u'briefing', u'car', u'card', u'crash', u'energy', u'exposed', u'firm', u'first', u'government', u'higher', u'hours', u'house', u'information', u'interest', u'korea', u'like', u'media', u'million', u'monday', u'new', u'north', u'one', u'paris', u'press', u'qatar', u'raised', u'rate', u'related', u'renewable', u'said', u'security', u'show', u'social', u'solar', u'tech', u'tourists', u'trump', u'ups', u'warmbier', u'week', u'white', u'year']
    [u'american', u'americans', u'bill', u'care', u'cuba', u'death', u'drug', u'duration', u'fees', u'fisher', u'government', u'health', u'house', u'human', u'june', u'korea', u'la', u'late', u'may', u'momentjs', u'monday', u'moreduration', u'new', u'north', u'otto', u'people', u'president', u'released', u'report', u'republicans', u'rights', u'said', u'says', u'see', u'statehood', u'states', u'syrian', u'time', u'told', u'trump', u'united', u'us', u'use', u'video', u'warmbier', u'white', u'woods', u'would', u'wrote', u'year']


## Sum up the counts of each vocabulary word for each kind of article


```python
import numpy as np

# Sum up the counts of each vocabulary word
dist = np.sum(train_data_features_wiki, axis=0)
dist2 = np.sum(train_data_features_cnn, axis=0)
dist3 = np.sum(train_data_features_nbc, axis=0)

# For each, print the vocabulary word and the number of times it 
# appears in the training set
for tag, count in zip(vocab_wiki, dist):
    tag =  unicodedata.normalize('NFKD', tag).encode('ascii','ignore')
    print(count, tag)
    
print('**************************************************')    
for tag, count in zip(vocab_cnn, dist2):
    tag =  unicodedata.normalize('NFKD', tag).encode('ascii','ignore')
    print(count, tag)
    
    
print('**************************************************')       
for tag, count in zip(vocab_nbc, dist):
    tag =  unicodedata.normalize('NFKD', tag).encode('ascii','ignore')
    print(count, tag)
```

    (8, 'air')
    (8, 'also')
    (9, 'american')
    (9, 'band')
    (12, 'born')
    (10, 'company')
    (6, 'congress')
    (8, 'county')
    (6, 'december')
    (12, 'dimle')
    (15, 'first')
    (8, 'football')
    (7, 'four')
    (7, 'high')
    (6, 'january')
    (6, 'latin')
    (7, 'located')
    (7, 'many')
    (7, 'march')
    (8, 'mellotronen')
    (7, 'mi')
    (10, 'music')
    (8, 'naval')
    (14, 'new')
    (14, 'one')
    (6, 'program')
    (6, 'public')
    (9, 'puerto')
    (6, 'record')
    (7, 'released')
    (6, 'rico')
    (14, 'rock')
    (12, 'school')
    (6, 'season')
    (6, 'single')
    (8, 'song')
    (6, 'stadium')
    (8, 'states')
    (8, 'station')
    (8, 'television')
    (7, 'th')
    (9, 'three')
    (8, 'time')
    (8, 'tredinnick')
    (10, 'two')
    (9, 'united')
    (6, 'universal')
    (9, 'uss')
    (6, 'village')
    (7, 'years')
    **************************************************
    (13, 'air')
    (8, 'airways')
    (12, 'also')
    (10, 'amazon')
    (13, 'american')
    (11, 'back')
    (7, 'billion')
    (8, 'boeing')
    (12, 'briefing')
    (12, 'car')
    (10, 'card')
    (9, 'crash')
    (12, 'energy')
    (9, 'exposed')
    (9, 'firm')
    (18, 'first')
    (7, 'government')
    (9, 'higher')
    (10, 'hours')
    (20, 'house')
    (9, 'information')
    (16, 'interest')
    (10, 'korea')
    (11, 'like')
    (13, 'media')
    (12, 'million')
    (15, 'monday')
    (9, 'new')
    (12, 'north')
    (8, 'one')
    (14, 'paris')
    (9, 'press')
    (12, 'qatar')
    (10, 'raised')
    (10, 'rate')
    (13, 'related')
    (9, 'renewable')
    (19, 'said')
    (9, 'security')
    (8, 'show')
    (13, 'social')
    (9, 'solar')
    (9, 'tech')
    (8, 'tourists')
    (12, 'trump')
    (8, 'ups')
    (10, 'warmbier')
    (9, 'week')
    (21, 'white')
    (9, 'year')
    **************************************************
    (8, 'american')
    (8, 'americans')
    (9, 'bill')
    (9, 'care')
    (12, 'cuba')
    (10, 'death')
    (6, 'drug')
    (8, 'duration')
    (6, 'fees')
    (12, 'fisher')
    (15, 'government')
    (8, 'health')
    (7, 'house')
    (7, 'human')
    (6, 'june')
    (6, 'korea')
    (7, 'la')
    (7, 'late')
    (7, 'may')
    (8, 'momentjs')
    (7, 'monday')
    (10, 'moreduration')
    (8, 'new')
    (14, 'north')
    (14, 'otto')
    (6, 'people')
    (6, 'president')
    (9, 'released')
    (6, 'report')
    (7, 'republicans')
    (6, 'rights')
    (14, 'said')
    (12, 'says')
    (6, 'see')
    (6, 'statehood')
    (8, 'states')
    (6, 'syrian')
    (8, 'time')
    (8, 'told')
    (8, 'trump')
    (7, 'united')
    (9, 'us')
    (8, 'use')
    (8, 'video')
    (10, 'warmbier')
    (9, 'white')
    (6, 'woods')
    (9, 'would')
    (6, 'wrote')
    (7, 'year')


## save the data in csv file


```python
import pandas as pd
columns = ['text' , 'type']
data_pair = [()]
for value in wiki_array:
    data_pair.append(('wiki',value))

for value in cnn_array:
    data_pair.append(('cnn',value))
        
for value in nbc_array:
    data_pair.append(('nbc',value))
len(data_pair)
df = pd.DataFrame(data=data_pair, columns=['text','type'])
df.to_csv("data.csv",index = False)
```


```python

```
