# detect_human_names
It is function which is written to detect human names in sentences.



		import spacy

		spacy.prefer_gpu()
		nlp = spacy.load("en_core_web_sm")
		survey_text = input('Input your string here: ')


		def get_person_names(nlp_doc):
		    result=[]
		    for ent in nlp_doc:
			if ent.ent_iob != 0 and ent.ent_type_ == 'PERSON':
			    result.append(ent.string)

		    return result

		def redact_names(nlp_doc):
		    for ent in nlp_doc.ents:
			ent.merge()
		    result=get_person_names(nlp_doc)
		    return result

		survey_doc = nlp(unicode(survey_text))
		print(redact_names(survey_doc))
