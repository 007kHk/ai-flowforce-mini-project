# 🎲 Randomizer Toolkit (Streamlit)

import streamlit as st
import random
import base64

st.set_page_config(page_title="Randomizer Toolkit", page_icon="🎲")
st.title("🎲 Randomizer Toolkit")
st.write("Create lists, pick randomly, and make fast decisions!")

# --- Input UI ---
st.subheader("📝 Enter Your List")
custom_items = st.text_area("Add items (one per line):", height=150)

# --- Optional Category Label ---
category = st.text_input("Optional: Category or Title")

# --- Randomize Button ---
if st.button("🎲 Pick One"):
    if not custom_items.strip():
        st.warning("Please enter at least one item.")
    else:
        items = [line.strip() for line in custom_items.strip().split("\n") if line.strip()]
        result = random.choice(items)
        st.success(f"**Random Pick:** {result}")

        if category:
            content = f"Category: {category}\nList: {', '.join(items)}\nChosen Item: {result}"
        else:
            content = f"List: {', '.join(items)}\nChosen Item: {result}"

        # Generate Download Link
        b64 = base64.b64encode(content.encode()).decode()
        href = f'<a href="data:file/txt;base64,{b64}" download="random_choice.txt">📥 Download This Pick</a>'
        st.markdown(href, unsafe_allow_html=True)

# --- Tips ---
st.sidebar.header("💡 Tips")
st.sidebar.markdown("- Use it for team names, tasks, rewards")
st.sidebar.markdown("- Add funny or themed entries")
st.sidebar.markdown("- Keep past picks saved")
