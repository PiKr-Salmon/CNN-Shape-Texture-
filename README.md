# CNN-Shape-Texture-

การออกแบบการทดลอง (Experimental Design)
1. การสร้างเงื่อนไขของชุดข้อมูลทดสอบ (Test Conditions):
   - Original Test Set: ภาพปกติที่มีทั้ง Local Texture และ Global
   - ShapePatch-Shuffled Test Set (Texture Preserved / Shape Destroyed): แบ่งภาพเป็นกริดขนาด Z px X Z px (รวม Z^2 ชิ้น) แล้วสลับตำแหน่งอย่างสุ่ม กระบวนการนี้ทำลาย Global Shape และความต่อเนื่องของเส้น
     ขอบลงอย่างสิ้นเชิง แต่ Local Texture ของวัตถุภายในแต่ละ Patch ยังคงเดิม
   - Edge-Extracted Test Set (Shape Preserved / Texture Removed): แปลงภาพด้วย Sobel Edge Detector หรือ Canny Filter ร่วมกับ Grayscale เพื่อลบสีและลวดลายสถิติระดับพิกเซล เหลือเพียง Global Shape /
     Structure
2. การเปรียบเทียบเงื่อนไขโมเดล (Model Conditions):
   - Condition A (Baseline Pre-trained Model): ใช้ Model ที่ Pre-train บน ImageNet โดยไม่มีการปรับแต่งเพิ่มเติม
   - Condition B (Fine-tuned Shape-Promoted Model): นำ Model มา Fine-tune บน STL-10 Training Set โดยใช้ Data Augmentation ที่ทำลาย Texture (ผสมภาพปกติกับภาพ Patch-Shuffled และ Edge
     Images) เพื่อบังคับให้โมเดลค้นหาฟีเจอร์เชิงโครงร่าง (Shape) ในการจำแนกคลาส
