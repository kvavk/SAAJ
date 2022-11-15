import csv
import ijson


### SARC Directory Paths ###
SARC_DATA = '/n/fs/nlpdatasets/SARC/2.0/'
SARC_MAIN = SARC_DATA + 'main/'
SARC_POL = SARC_DATA + 'pol/'


def load_sarc_responses(train_file, test_file, comment_file, max=None, lower=True):
  '''loads SARC data from csv files
  Args:
    train_file: csv file with train sequences
    test_file: csv file with train sequences
    comment_file: json file with details about all comments
    lower: boolean; if True, converts comments to lowercase
  Returns:
    train_sequences, train_labels, test_sequences, test_labels
    train_sequences: {'ancestors': list of ancestors for all sequences,
                      'responses': list of responses for all sequences}
    train_labels: list of labels for responses for all sequences.
  '''

  with open(comment_file, 'rb') as f:
  
    train_docs = {'ancestors': [], 'responses': []}
    train_labels = []
    with open(train_file, 'r') as f:
      reader = csv.reader(f, delimiter='|')
      comments = ijson.items(f, "item")
      counter = 0
      for row in reader:
        ancestors = row[0].split(' ')
        print(ancestors)
        responses = row[1].split(' ')
        print(responses)
        labels = row[2].split(' ')
        if lower:
          train_docs['ancestors'].append([r['text'].lower() for r in comments if r in ancestors])
          train_docs['responses'].append([r['text'].lower() for r in comments if r in responses])
        else:
          train_docs['ancestors'].append([r['text'] for r in comments if r in ancestors])
          train_docs['responses'].append([r['text'] for r in comments if r in responses])
        train_labels.append(labels)
        counter += 1
        print(counter)

    test_docs = {'ancestors': [], 'responses': []}
    test_labels = []
    with open(test_file, 'r') as f:
      reader = csv.reader(f, delimiter='|')
      counter = 0
      for row in reader:
        ancestors = row[0].split(' ')
        responses = row[1].split(' ')
        labels = row[2].split(' ')
        if lower:
          test_docs['ancestors'].append([r['text'].lower() for r in comments if r in ancestors])
          test_docs['responses'].append([r['text'].lower() for r in comments if r in responses])
        else:
          test_docs['ancestors'].append([r['text'] for r in comments if r in ancestors])
          test_docs['responses'].append([r['text'] for r in comments if r in responses])
        test_labels.append(labels)
        counter += 1
        print(counter)

  return train_docs, test_docs, train_labels, test_labels
