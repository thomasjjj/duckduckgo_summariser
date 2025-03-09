import streamlit as st
from duckduckgo_search import DDGS

def search_and_summarise(query, max_results=10, model="gpt-4o-mini"):
    # Initialise the DDGS class for DuckDuckGo search
    ddgs = DDGS()

    # Perform a text search for the query
    search_results = ddgs.text(query, max_results=max_results)

    # Combine the search results into a formatted string
    combined_results = ""
    for result in search_results:
        title = result.get("title", "No Title")
        url = result.get("href", "No URL")
        snippet = result.get("body", "No description available")
        combined_results += f"Title: {title}\nURL: {url}\nSnippet: {snippet}\n\n"

    # Prepare a prompt to instruct the AI to summarise the results
    prompt = ("Please summarise the following search results. "
              "Only use the information provided:\n\n" + combined_results)

    # Use the chat() method to get a summary of the results
    summary = ddgs.chat(prompt, model=model)

    return summary

def main():
    st.title("DuckDuckGo Search Summariser")
    st.write("Enter your search term below and the application will provide a summary of the search results.")

    query = st.text_input("Search Term:")
    max_results = st.number_input("Maximum Results", min_value=1, max_value=50, value=5, step=1)

    if st.button("Search and Summarise"):
        if query:
            with st.spinner("Searching and summarising..."):
                summary_text = search_and_summarise(query, max_results=int(max_results))
                st.subheader("Summary of Search Results:")
                st.text_area("", summary_text, height=300)
        else:
            st.warning("Please enter a search term.")

if __name__ == "__main__":
    main()
