import streamlit as st
import pandas as pd

# ตั้งค่าหน้าเว็บ
st.set_page_config(page_title="Stock Checker System", icon="📦")

st.title("📦 ระบบเช็คสต็อกสินค้าอัจฉริยะ")
st.info("คำแนะนำ: ไฟล์ Excel ควรมีคอลัมน์ชื่อ 'รายการ' และ 'คงเหลือ'")

# ส่วนอัปโหลดไฟล์
uploaded_file = st.file_uploader("โยนไฟล์ Excel (.xlsx) ลงที่นี่", type=["xlsx"])

if uploaded_file:
    # อ่านข้อมูลจาก Excel
    df = pd.read_excel(uploaded_file)
    
    # ส่วนค้นหาด่วน
    search_query = st.text_input("🔍 ค้นหาชื่อสินค้า...")
    if search_query:
        df = df[df['รายการ'].str.contains(search_query, na=False)]

    # สรุปภาพรวม
    col1, col2 = st.columns(2)
    with col1:
        st.metric("รายการทั้งหมด", len(df))
    with col2:
        low_stock_count = len(df[df['คงเหลือ'] < 5]) # สมมติว่าน้อยกว่า 5 คือใกล้หมด
        st.metric("สินค้าใกล้หมด", low_stock_count, delta_color="inverse")

    # แสดงตารางข้อมูล
    st.subheader("📊 ตารางสต็อกปัจจุบัน")
    st.dataframe(df, use_container_width=True)
    
    # ปุ่ม Export เป็น CSV (เผื่อเอาไปทำต่อ)
    csv = df.to_csv(index=False).encode('utf-8-sig')
    st.download_button("📥 ดาวน์โหลดรายงานนี้", data=csv, file_name="stock_report.csv", mime="text/csv")
