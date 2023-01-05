# Agenda 
- What is an Entity?
- Why Entity?
- What identifies as a Entity?
- In Amelia what is a Data?
- Every Token is a Data. Based on your Entity Tagger each token can be a entity.
- Entity has nothing to do with Meaning but has something to do with meaning -> True or False
- Grouping Meaningless Tokens and Tokens with similar meanings <- NER

# Tokens

- What are tokens?
    - A word is a token. 

- Basic Tokenizer
    - Spilt statements by ' ' and convert all words to lower case

- eg: I want to reset my password.

        I           | i
        want        | want
        to          | to
        reset       | reset
        my          | my
        password    | password

# Grouping Tokens

- Spelling -> (bangalore, bangalore)
- Meaning -> (See, seen) -> Lemmatiztion  X -> (bangalore, bengaluru, Barath,Bharath,Barat)

- Characterstics -> (a, an, the), (STOP_WORDS)

# Handling Nouns -> Phonetic Hashing (American Soundex)
    b, f, p, v → 1 
    c, g, j, k, q, s, x, z → 2 
    d, t → 3 
    l → 4 
    m, n → 5
    r → 6 
    h, w, y → Not Coded

    bangalore  -> B524   |  Ajay   -> A2  | Shrivastava -> S612
    bengaluru  -> B524   |  Ajai -> A2    | Srivastav -> S612

# Q&A

- Mumbai & Bombay  (NOUNS -> Same Meaning different spelling and Vice versa)


# NER (NAMED ENTITY RECOGNITION)  

- CREATE IOB SAMPLES -> BLACK BOX (ML MODEL, DL MODEL, STATISTICAL MODEL) -> IOB LABELS -> EXTRACT ENTITY LOCATION

# IOB SAMPLES

    B -> Begining of an Entity
    I -> Intermediate Part of an Entity
    O -> Out of Scope

    eg.: Create IOB for tagging Person Name

    My name is Barath

    my      |   O
    name    |   O
    is      |   O
    barath  |   B

    I think Vishal Kulkarni is a Badass boss.

    i           | O
    think       | O
    vishal      | B
    kulkarni    | I
    is          | O
    a           | O
    badass      | O
    boss        | O

    We all know that Purushothaman Narayanan and Vishal Kulkarni are best buddies.

    we                  | O
    all                 | O
    know                | O
    that                | O
    purushothaman       | B
    narayanan           | I
    and                 | O
    vishal              | B
    kulkarni            | I
    are                 | O
    best                | O
    buddies             | O


Train the model on these IOB data with MSE

# CRF (Custom Random Fields)


- DEFINE FEATURES -> CREATE TRAINING SAMPLES -> BLACK BOX (ML MODEL, DL MODEL, STATISTICAL MODEL) -> EXTRACT ENTITY LOCATION

FEATURES
- First name will be prefixed with '_*that*_' <-> F1
- Last name will follow First Name <-> F2

        eg:
            We all know that Purushothaman Narayanan and Vishal Kulkarni are best buddies.
                                | F1 | F2|
            we                  | 0  | 0 |
            all                 | 0  | 0 |
            know                | 0  | 0 |
            that                | 0  | 0 |
            purushothaman       | 1  | 0 |
            narayanan           | 0  | 1 |
            and                 | 0  | 0 |
            vishal              | 0  | 0 |
            kulkarni            | 0  | 1 |
            are                 | 0  | 0 |
            best                | 0  | 0 |
            buddies             | 0  | 0 |
