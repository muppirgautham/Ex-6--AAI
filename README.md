## NAME: M Gautham
## REGISTER NO: 212221230027
## EX. NO: 5
## DATE: 24/04/24
<H1 ALIGN =CENTER>Implementation of Semantic ANalysis</H1>
<H3>Aim: to perform Parts of speech identification and Synonym using Natural Language Processing (NLP) techniques. </H3> 
 <BR>
<h3>Algorithm:</h3>
Step 1: Import the nltk library.<br>
Step 2: Download the 'punkt', 'wordnet', and 'averaged_perceptron_tagger' resources.<br>
Step 3:Accept user input for the text.<br>
Step 4:Tokenize the input text into words using the word_tokenize function.<br>
Step 5:Iterate through each word in the tokenized text.<br>
•	Perform part-of-speech tagging on the tokenized words using nltk.pos_tag.<br>
•	Print each word along with its corresponding part-of-speech tag.<br>
•	For each verb , iterate through its synsets (sets of synonyms) using wordnet.synsets(word).<br>
•	Extract synonyms and antonyms using lemma.name() and lemma.antonyms()[0].name() respectively.<br>
•	Print the unique sets of synonyms and antonyms.
<H3>Program:</H3>

```
Name: M gautham
Register No: 212221230027
```

```
import nltk
from nltk.corpus import wordnet

nltk.download('averaged_perceptron_tagger')
nltk.download('wordnet')
nltk.download('punkt')

# Function to identify verbs in a sentence
def get_verbs(sentence):
    verbs = []
    pos_tags = nltk.pos_tag(nltk.word_tokenize(sentence))
    for word, tag in pos_tags:
        if tag.startswith('V'):  # Verbs start with 'V' in the POS tag
            verbs.append(word)
    return verbs


def get_synonyms(word):
    synonyms = []
    for syn in wordnet.synsets(word):
        for lemma in syn.lemmas():
            synonyms.append(lemma.name())
    return synonyms


def read_text_file(file_path):
    with open(file_path, 'r') as file:
        text = file.read()
    return text


def main():
    file_path = 'sample.txt'

    text = read_text_file(file_path)
    sentences = nltk.sent_tokenize(text)

    all_verbs = []
    synonyms_dict = {}

    for sentence in sentences:
        verbs = get_verbs(sentence)
        all_verbs.extend(verbs)
        for verb in verbs:
            synonyms = get_synonyms(verb)
            synonyms_dict[verb] = synonyms

    with open('output.csv', 'w', newline='') as csvfile:
        writer = csv.writer(csvfile)
        writer.writerow(['Verb', 'Synonyms'])
        for verb, synonyms in synonyms_dict.items():
            writer.writerow([verb, ', '.join(synonyms)])


if __name__ == '__main__':
    main()
```

<H3>Output</H3>

|Verb|Synonyms|
|---|---|
|remember|remember, retrieve, recall, call\_back, call\_up, recollect, think, remember, think\_of, remember, think\_back, remember, remember, commend, remember, remember, commemorate, remember|
|was|Washington, Evergreen\_State, WA, be, be, be, exist, be, be, equal, be, constitute, represent, make\_up, comprise, be, be, follow, embody, be, personify, be, be, live, be, cost, be|
|playing|playing, playing, acting, playing, playacting, performing, play, play, play, act, play, represent, play, play, spiel, play, act, play, act\_as, play, play, play, recreate, play, play, play, play, play, toy, play, play, run, toy, fiddle, diddle, play, play, dally, trifle, play, play, dally, toy, play, flirt, play, act, play, roleplay, playact, play, bring, work, play, wreak, make\_for, play, play, bet, wager, play, play, play, play, meet, encounter, play, take\_on, play|
|beat|beat, round, pulse, pulsation, heartbeat, beat, rhythm, beat, musical\_rhythm, beat, beatnik, beat, beat, meter, metre, measure, beat, cadence, beat, beat, beat, beat, beat\_out, crush, shell, trounce, vanquish, beat, beat\_up, work\_over, beat, beat, pound, thump, beat, drum, beat, thrum, beat, beat, flap, beat, beat, scramble, beat, beat, beat, bunk, tick, ticktock, ticktack, beat, beat, flap, beat, pulsate, beat, quiver, beat, beat, beat, outwit, overreach, outsmart, outfox, beat, circumvent, perplex, vex, stick, get, puzzle, mystify, baffle, beat, pose, bewilder, flummox, stupefy, nonplus, gravel, amaze, dumbfound, exhaust, wash\_up, beat, tucker, tucker\_out, all\_in, beat, bushed, dead|
|called|name, call, call, call, telephone, call\_up, phone, ring, shout, shout\_out, cry, call, yell, scream, holler, hollo, squall, call, send\_for, visit, call\_in, call, call, call, call, call, call, address, call, call, call, call\_in, bid, call, call, call\_off, call, predict, foretell, prognosticate, call, forebode, anticipate, promise, call, call, call, call, call, call, call, call, call, call|
|said|state, say, tell, allege, aver, say, suppose, say, read, say, order, tell, enjoin, say, pronounce, articulate, enounce, sound\_out, enunciate, say, say, say, say, say, say, aforesaid, aforementioned, said|
|am|americium, Am, atomic\_number\_95, Master\_of\_Arts, MA, Artium\_Magister, AM, amplitude\_modulation, AM, be, be, be, exist, be, be, equal, be, constitute, represent, make\_up, comprise, be, be, follow, embody, be, personify, be, be, live, be, cost, be|
|bored|bore, tire, bore, drill, bored, world-weary, blase, bored|
|don|Don, preceptor, don, don, father, Don, Don, Don\_River, Don, wear, put\_on, get\_into, don, assume|
|want|privation, want, deprivation, neediness, lack, deficiency, want, need, want, wish, wishing, want, desire, want, want, need, require, want, want, want|
|play|play, drama, dramatic\_play, play, play, maneuver, manoeuvre, play, play, play, bid, play, play, child's\_play, playing\_period, period\_of\_play, play, free\_rein, play, shimmer, play, fun, play, sport, looseness, play, play, frolic, romp, gambol, caper, turn, play, gambling, gaming, play, play, swordplay, play, play, play, act, play, represent, play, play, spiel, play, act, play, act\_as, play, play, play, recreate, play, play, play, play, play, toy, play, play, run, toy, fiddle, diddle, play, play, dally, trifle, play, play, dally, toy, play, flirt, play, act, play, roleplay, playact, play, bring, work, play, wreak, make\_for, play, play, bet, wager, play, play, play, play, meet, encounter, play, take\_on, play|
|got|get, acquire, become, go, get, get, let, have, receive, get, find, obtain, incur, arrive, get, come, bring, get, convey, fetch, experience, receive, have, get, pay\_back, pay\_off, get, fix, have, get, make, induce, stimulate, cause, have, get, make, get, catch, capture, grow, develop, produce, get, acquire, contract, take, get, get, make, get, drive, get, aim, catch, get, catch, arrest, get, get, catch, get, get, get, catch, get, catch, get, get, receive, scram, buzz\_off, fuck\_off, get, bugger\_off, get, get, get\_under\_one's\_skin, get, catch, get, draw, get, get, perplex, vex, stick, get, puzzle, mystify, baffle, beat, pose, bewilder, flummox, stupefy, nonplus, gravel, amaze, dumbfound, get\_down, begin, get, start\_out, start, set\_about, set\_out, commence, suffer, sustain, have, get, beget, get, engender, father, mother, sire, generate, bring\_forth|
|’||
|go|go, spell, tour, turn, Adam, ecstasy, XTC, go, disco\_biscuit, cristal, X, hug\_drug, crack, fling, go, pass, whirl, offer, go, go\_game, travel, go, move, locomote, go, proceed, move, go, go\_away, depart, become, go, get, go, run, go, run, go, pass, lead, extend, proceed, go, go, go, sound, go, function, work, operate, go, run, run\_low, run\_short, go, move, go, run, survive, last, live, live\_on, go, endure, hold\_up, hold\_out, go, die, decease, perish, go, exit, pass\_away, expire, pass, kick\_the\_bucket, cash\_in\_one's\_chips, buy\_the\_farm, conk, give-up\_the\_ghost, drop\_dead, pop\_off, choke, croak, snuff\_it, belong, go, go, start, go, get\_going, move, go, go, go, blend, go, blend\_in, go, lead, fit, go, rifle, go, go, plump, go, fail, go\_bad, give\_way, die, give\_out, conk\_out, go, break, break\_down, go|
|sleep|sleep, slumber, sleep, sopor, sleep, nap, rest, eternal\_rest, sleep, eternal\_sleep, quietus, sleep, kip, slumber, log\_Z's, catch\_some\_Z's, sleep|
|‘||
|s|second, sec, s, sulfur, S, sulphur, atomic\_number\_16, south, due\_south, southward, S, mho, siemens, reciprocal\_ohm, S, S, s, randomness, entropy, S|
|win\.||
|sat|Saturday, Sabbatum, Sat, sit, sit\_down, sit, sit\_around, sit\_down, sit, sit, model, pose, sit, posture, ride, sit, sit, baby-sit, sit, seat, sit, sit\_down, sit|
|played|play, play, play, act, play, represent, play, play, spiel, play, act, play, act\_as, play, play, play, recreate, play, play, play, play, play, toy, play, play, run, toy, fiddle, diddle, play, play, dally, trifle, play, play, dally, toy, play, flirt, play, act, play, roleplay, playact, play, bring, work, play, wreak, make\_for, play, play, bet, wager, play, play, play, play, meet, encounter, play, take\_on, play, played|
|won|South\_Korean\_won, won, North\_Korean\_won, won, win, acquire, win, gain, gain, advance, win, pull\_ahead, make\_headway, get\_ahead, gain\_ground, succeed, win, come\_through, bring\_home\_the\_bacon, deliver\_the\_goods, won|
|yawned|yawn, gape, yawn, yaw|

<H3>Result:</H3>
Thus ,the program to perform the Parts of Speech identification and Synonymis executed sucessfully.
