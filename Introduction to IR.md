# Chapter 1: Introduction to IR
- Database != Web Search (IR)
	- Database เมื่อค้นหาแล้วไม่เจอเป๊ะ ๆ 100% จะไม่ return ค่าใด ๆ 
	- Web Search จะ return ค่าแทบทุกครั้ง โดยไล่ค่าที่เกี่ยวข้องที่สุดออกมาก่อน
- IR: Representation, storage and access to information items
	- Focus on information and user need
-
## Database vs IR
#### DB
Structured, Clear and semantics field, using defined query language, Must be able to do recovery, Matching exacted result
#### IR
Unstructured, No fields, Search with free text, downplayed (still and issue) = เป็นไปได้ยาก, Imprecise matching

TODO: Convert to table
|point| DB | IR |
|----|----|----|
| Data|Structured|Unstructured|
|Semantic| Semantic|No fields|
|query| SQL, NoSQL|Free text|


### IR System
- Intepret content of information items
- Generate **ranking** (จัดลำดับ) + Notion of **relevant** (ความตรงประเด็น) ** **สำคัญที่สุด**
- Relevance
	- Precision: ผลลัพธ์ตรงประเด็น / ผลลัพธ์ทั้งหมดที่ได้ออกมา *หาง่าย* 
	- Recall: ผลลัพธ์ตรงประเด็น / ผลลัพธ์ที่ตรงประเด็นทั้งหมด *หายากกว่า*
### Relevance
- เกี่ยวข้อง, ทันสมัย, แหล่งน่าเชื่อถือ, ตรงความต้องการผู้ใช้งาน
### Problem with Keywords
- ไม่ครอบคลุม synnonym EX: prc/china, restaurant/cafe
	- ต้องมีลิสต์ของ synnoym ทั้งหมดเพื่อให้ครอบคลุม
- ได้ผลลัพธ์ที่ไม่เกี่ยวข้องกรณีคำกำกวม (ambigous) EX: bat=ค้างคาว/ไม้เบสบอล, Apple=บริษัท/ผลไม้, bit=การกิน/หน่วยของข้อมูล
	- ต้องการข้อมูลเพิ่มเติมจากผู้ใช้งานเพื่อให้เข้าใจ context มากขึ้น

### Basic Concepts
#### Retrieval vs Browsing
- Retrieval
	- Information, Purposeful
	- เป้าหมายชัดเจน ต้องการข้อมูลเฉพาะเจาะจง
- Browsing
	- Glancing around
	- Main objective not clear in the beginning
	- Purpose might change!
	- คลิกลิงก์ไปเรื่อย ๆ EX: อ่านบทความวิกิพีเดียแล้วกดลิงก์ในบทความซ้ำ ๆ ไปเรื่อย ๆ (เห้ย น่าสนใจดี ลองดูเพิ่มดีกว่า) เป็นต้น, ค้น วัดพระแก้ว -> คนจีน -> ปักกิ่ง -> อู่ฮั่น -> โควิด
#### Indexing
Docs -> (+ Structure->) Accent Spacing -> stopwords -> Noun groups -> Stemming -> Manual Indexing
- การทำ indexing ทำให้ค้นข้อมูลได้ง่ายขึ้น
	- Docs = เอกสารตั้งต้น
	- Structure = การวิเคราะห์โครงสร้างเอกสาร EX: สารบัญ
	- Accent Spacing = แบ่งช่องว่างระหว่างคำ แยกเป็นคำ/ประโยคให้ชัดเจน
	- Stopwords = ตัดคำไม่มีความหมายทิ้ง EX: This is a book -> เหลือแค่ Book (ตัด adj, adv, prep)
	- Noun groups = ผลลัพธ์คำนามจากการตัด Stopwords
	- Stemming = การนำคำที่เกิดมาจาก "รากศัพท์" เดียวกันจัดรวมกัน EX: Go, Gone, Going (อาจมองเป็นการจัดหมวดหมู่ index ด้วยก็ได้ EX: ปุ๋ย, ยาฆ่าแมลง, น้ำ = หมวดหมู่เกษตรกรรม หรือ วาเลนไทน์, ความรัก, ชอคโกแลต, แฟน = ความรัก เป็นต้น ทั้งนี้อาจจัดได้หลายแบบ)

### IR Concept
- Computer Center View: สร้างระบบไว้ก่อน ให้ผู้ใช้ไปศึกษาใช้เอง **เรียนอันนี้**
- Human Center View: คนต้องการอะไร สร้างระบบให้รองรับ+เรียนรู้
### IR Questions
1. Transalating user need: แปลงคำค้นหาผู้ใช้อย่างไร ให้คอมเข้าใจ
		ข้อมูลบางอย่างถ้าค้นตาม keyword เฉย ๆ อาจไม่เหมาะเช่น not dog ผู้ใช้ต้องการค้นข้อมูลที่ไม่เกี่ยวกับสุนัข แต่คอมอาจเข้าใจว่าให้ค้นเอกสารที่มี index ว่า not dog
2. Using indices: ทำ index อย่างไร + ค้น index อย่างไร
3. Ranking: จัดลำดับความ relevant ข้อมูล (ให้คะแนนข้อมูล)
		EX: ข้อมูลที่มีคำค้นอยู่ใกล้เคียงกันได้คะแนนมากกว่า EX: ค้นว่า not dog ข้อมูลที่มีข้อความ not absdfasdfadgdfsadsdfs dog ได้คะแนนน้อยกว่า not asdf dog, ข้อมูลที่มีคำค้นหาเรียงตามลำดับที่ค้น ได้คะแนนมากกว่า EX: ค้นว่า cat dog ข้อมูลทีเ่ป็นคำว่า cat asdf dog ได้คะแนนมากกว่า dog asdf cat, ข้อมูลที่ตรง keyword ค้นหาได้คะแนนมากกว่า EX: ค้นว่า cat dog ข้อมูลที่เป็น cat asdf dog ได้คะแนนมากกว่า cat asdf

### Nowadays vs What we're learning,
การเรียนการสอนปกติเราจะใช้ text ในการเรียน แต่ยุคปัจจุบันมีข้อมูลหลายแบบไม่ว่าจะเป็นรูป วิดิโอ สื่อต่าง ๆ  ทั้งนี้สามารถประยุกต์ได้