## Natural Language Understanding with RASA
https://nlu.rasa.ai/tutorial.html

Estruturação de intenções e entendidas a partir de solução com exemplo de boleto.

### Install

> Debian
```{shell, engine='bash', count_lines}
sudo apt-get update
sudo apt-get install python-dev -y
sudo apt-get install python-pip -y
```

> Centos
```{shell, engine='bash', count_lines}
sudo yum install python-devel
```

> RASA

```{shell, engine='bash', count_lines}
sudo pip install rasa_nlu
sudo pip install -U scikit-learn scipy sklearn-crfsuite
sudo pip install spacy
sudo pip install sklearn

#IF ERROR
pip install --upgrade --force-reinstall sklearn
```

## Download Language Models

```{shell, engine='bash', count_lines}
sudo python -m spacy download en
sudo python -m spacy download pt
```

### Training
```{shell, engine='bash', count_lines}
python -m rasa_nlu.train -c config/config_spacy.json
python -m rasa_nlu.server -c config/config_spacy.json
```

>> https://github.com/RasaHQ/rasa-nlu-trainer
>> https://rasahq.github.io/rasa-nlu-trainer

## Server HTTP

### Request

> Raw POST sample as JSON

http://<server>/parse

```json
{"q":"quero gerar o boleto de janeiro"}
```

### Output
```json
{
  "entities": [
    {
      "start": 14, 
      "extractor": "ner_crf", 
      "end": 20, 
      "value": "boleto", 
      "entity": "boleto"
    }, 
    {
      "start": 21, 
      "extractor": "ner_crf", 
      "end": 31, 
      "value": "de janeiro", 
      "entity": "mes"
    }
  ], 
  "intent": {
    "confidence": 0.6182224263214309, 
    "name": "findBoletoDASByMes"
  }, 
  "text": "quero gerar o boleto de janeiro", 
  "intent_ranking": [
    {
      "confidence": 0.6182224263214309, 
      "name": "findBoletoDASByMes"
    }, 
    {
      "confidence": 0.2125461695864951, 
      "name": "goodbye"
    }, 
    {
      "confidence": 0.12601956063941733, 
      "name": "findBoletoDAS"
    }, 
    {
      "confidence": 0.04321184345265633, 
      "name": "greet"
    }
  ]
}
```