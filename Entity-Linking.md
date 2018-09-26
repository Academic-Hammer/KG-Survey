# Entity Linking

## TODO

- Definition of mention and entity.

## Summary

### [Entity Linking via Joint Encoding of Types , Descriptions , and Context](http://www.aclweb.org/anthology/D17-1284) [EMNLP2017, cites=14]

**Main Idea**: Use multiple sources of information to learn the representation of the entity: description, contexts around its mentions, and its fine-grained types.

**Method**:

**Encoders**:
- Mention Context Encoder: For local context,concatenate LSTM(w_1, ..., m) and LSTM(m, ..., w_N). For *document context (?)*, a single layer feed-forward network on the top of a bag-of-mention surfaces representation. Then concatenate them and pass them through another single layer feed-forward network. p(e|m) = softmax(v_m, v_e)
- Entity Description Encoder: a CNN to encode the description of the entity. p(e|desc) is same as above.
- Type Encoder: Directly give the type representation. P(t|e) = sigmoid(v_t, v_e)
- Type-Aware Context Encoder: Predict the type of given context. P(t|m) = sigmoid(v_t, v_m)

(I think description representation is useless. Predicting type is a good way to learn context representation v_m but there is no overlay between v_m and v_desc? Maybe v_e?)

**Linking**:
P(e|m) = P_prior(e|m) + P_text(e|m) - ( P_prior(e|m) * P_text(e|m) )

where P_prior is normalized frequency of entities on given mentions using Cross-Wikis. (a dictionary computed from a Google crawl of the web that stores the frequency with which a mention links to a particular entity.)

(There is no explanation of the formula. I think it's incorrect.)
