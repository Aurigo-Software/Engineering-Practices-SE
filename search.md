---
layout: page
title: Search Handbook
permalink: /search/
description: Search across the entire Engineering Practices & Standards Handbook to find specific content, guides, templates, and best practices.
category: Navigation
tags: [search, find, discovery, content]
last_updated: 2024-11-06
show_sidebar: false
---

# Search Handbook

<div class="search-container">
  <div class="search-header">
    <h2>Find What You Need</h2>
    <p>Search across all handbook content including guides, templates, checklists, and best practices.</p>
  </div>

  <div class="search-form">
    <div class="search-input-container">
      <input type="search" id="search-input" placeholder="Enter search terms..." autocomplete="off" />
      <button type="button" id="search-button" aria-label="Search">
        <svg width="20" height="20" viewBox="0 0 16 16">
          <path d="M11.5 6.5a5 5 0 11-10 0 5 5 0 0110 0zm-.5 4.5a6 6 0 10-1.5 1.5L15 16.5 16.5 15l-5.5-4z"/>
        </svg>
      </button>
    </div>
    
    <div class="search-filters">
      <div class="filter-group">
        <label class="filter-label">Filter by:</label>
        <select id="category-filter" class="filter-select">
          <option value="">All Categories</option>
          <option value="development-practices">Development Practices</option>
          <option value="architecture-design">Architecture & Design</option>
          <option value="quality-assurance">Quality Assurance</option>
          <option value="devops-infrastructure">DevOps & Infrastructure</option>
          <option value="security-practices">Security Practices</option>
          <option value="team-processes">Team Processes</option>
          <option value="standards-guidelines">Standards & Guidelines</option>
          <option value="tools-technologies">Tools & Technologies</option>
          <option value="reference-materials">Reference Materials</option>
        </select>
      </div>
      
      <div class="filter-group">
        <select id="type-filter" class="filter-select">
          <option value="">All Types</option>
          <option value="guide">Guides</option>
          <option value="template">Templates</option>
          <option value="checklist">Checklists</option>
          <option value="reference">References</option>
          <option value="example">Examples</option>
        </select>
      </div>
      
      <div class="filter-group">
        <select id="role-filter" class="filter-select">
          <option value="">All Roles</option>
          <option value="developer">Developer</option>
          <option value="architect">Architect</option>
          <option value="devops">DevOps Engineer</option>
          <option value="qa">QA Engineer</option>
          <option value="manager">Engineering Manager</option>
        </select>
      </div>
    </div>
    
    <div class="search-suggestions">
      <span class="suggestions-label">Popular searches:</span>
      <button type="button" class="suggestion-tag" data-search="git workflow">Git Workflow</button>
      <button type="button" class="suggestion-tag" data-search="code review">Code Review</button>
      <button type="button" class="suggestion-tag" data-search="testing strategies">Testing Strategies</button>
      <button type="button" class="suggestion-tag" data-search="ci cd">CI/CD</button>
      <button type="button" class="suggestion-tag" data-search="security guidelines">Security Guidelines</button>
      <button type="button" class="suggestion-tag" data-search="architecture patterns">Architecture Patterns</button>
    </div>
  </div>

  <div id="search-results" class="search-results" style="display: none;">
    <div class="results-header">
      <h3 id="results-count">Search Results</h3>
      <div class="results-actions">
        <button type="button" id="clear-search" class="clear-button">Clear Search</button>
      </div>
    </div>
    <div id="results-container" class="results-container">
      <!-- Search results will be inserted here -->
    </div>
  </div>

  <div id="search-empty" class="search-empty" style="display: block;">
    <div class="empty-state">
      <svg class="empty-icon" width="64" height="64" viewBox="0 0 24 24">
        <path d="M15.5 14h-.79l-.28-.27A6.471 6.471 0 0 0 16 9.5 6.5 6.5 0 1 0 9.5 16c1.61 0 3.09-.59 4.23-1.57l.27.28v.79l5 4.99L20.49 19l-4.99-5zm-6 0C7.01 14 5 11.99 5 9.5S7.01 5 9.5 5 14 7.01 14 9.5 11.99 14 9.5 14z"/>
      </svg>
      <h3>Search the Handbook</h3>
      <p>Enter search terms above to find guides, templates, best practices, and more across all practice areas.</p>
      
      <div class="search-tips">
        <h4>Search Tips:</h4>
        <ul>
          <li><strong>Keywords</strong>: Try specific terms like "git", "testing", "deployment"</li>
          <li><strong>Phrases</strong>: Use quotes for exact phrases: "code review process"</li>
          <li><strong>Filters</strong>: Use the dropdown filters to narrow results</li>
          <li><strong>Categories</strong>: Browse by specific practice areas</li>
        </ul>
      </div>
    </div>
  </div>

  <div id="search-loading" class="search-loading" style="display: none;">
    <div class="loading-spinner"></div>
    <p>Searching handbook...</p>
  </div>
</div>

<!-- Search Index Data (This would normally be generated by Jekyll) -->
<script>
// Simple search functionality - in production, this would use a proper search index
const searchIndex = [
  {% for page in site.pages %}
  {% unless page.url contains '/assets/' or page.url contains '404' %}
  {
    title: {{ page.title | default: page.name | jsonify }},
    url: {{ page.url | jsonify }},
    content: {{ page.content | strip_html | truncatewords: 50 | jsonify }},
    category: {{ page.category | default: '' | jsonify }},
    tags: {{ page.tags | default: [] | jsonify }},
    description: {{ page.description | default: '' | jsonify }}
  },
  {% endunless %}
  {% endfor %}
].filter(item => item.title && item.url);

document.addEventListener('DOMContentLoaded', function() {
  const searchInput = document.getElementById('search-input');
  const searchButton = document.getElementById('search-button');
  const categoryFilter = document.getElementById('category-filter');
  const typeFilter = document.getElementById('type-filter');
  const roleFilter = document.getElementById('role-filter');
  const resultsContainer = document.getElementById('results-container');
  const resultsCount = document.getElementById('results-count');
  const searchResults = document.getElementById('search-results');
  const searchEmpty = document.getElementById('search-empty');
  const searchLoading = document.getElementById('search-loading');
  const clearSearch = document.getElementById('clear-search');
  const suggestionTags = document.querySelectorAll('.suggestion-tag');

  let searchTimeout;

  function performSearch() {
    const query = searchInput.value.toLowerCase().trim();
    const categoryFilter_value = categoryFilter.value;
    const typeFilter_value = typeFilter.value;
    const roleFilter_value = roleFilter.value;

    if (!query && !categoryFilter_value && !typeFilter_value && !roleFilter_value) {
      showEmptyState();
      return;
    }

    showLoading();

    // Simulate search delay for better UX
    setTimeout(() => {
      const results = searchIndex.filter(item => {
        let matches = true;

        // Text search
        if (query) {
          const searchableText = `${item.title} ${item.content} ${item.description}`.toLowerCase();
          matches = matches && searchableText.includes(query);
        }

        // Category filter
        if (categoryFilter_value && item.category) {
          matches = matches && item.category.toLowerCase().includes(categoryFilter_value);
        }

        // Type filter (check tags)
        if (typeFilter_value && item.tags) {
          matches = matches && item.tags.some(tag => tag.toLowerCase().includes(typeFilter_value));
        }

        // Role filter (check tags)
        if (roleFilter_value && item.tags) {
          matches = matches && item.tags.some(tag => tag.toLowerCase().includes(roleFilter_value));
        }

        return matches;
      });

      displayResults(results, query);
    }, 300);
  }

  function showLoading() {
    searchEmpty.style.display = 'none';
    searchResults.style.display = 'none';
    searchLoading.style.display = 'block';
  }

  function showEmptyState() {
    searchLoading.style.display = 'none';
    searchResults.style.display = 'none';
    searchEmpty.style.display = 'block';
  }

  function displayResults(results, query) {
    searchLoading.style.display = 'none';
    searchEmpty.style.display = 'none';
    searchResults.style.display = 'block';

    resultsCount.textContent = `${results.length} result${results.length !== 1 ? 's' : ''}`;
    
    if (results.length === 0) {
      resultsContainer.innerHTML = `
        <div class="no-results">
          <p>No results found for your search.</p>
          <p>Try adjusting your search terms or filters.</p>
        </div>
      `;
      return;
    }

    resultsContainer.innerHTML = results.map(result => `
      <div class="result-item">
        <h4 class="result-title">
          <a href="${result.url}">${highlightText(result.title, query)}</a>
        </h4>
        ${result.description ? `<p class="result-description">${highlightText(result.description, query)}</p>` : ''}
        <p class="result-excerpt">${highlightText(result.content, query)}</p>
        <div class="result-meta">
          ${result.category ? `<span class="result-category">${result.category}</span>` : ''}
          ${result.tags && result.tags.length > 0 ? `<span class="result-tags">${result.tags.slice(0, 3).join(', ')}</span>` : ''}
        </div>
      </div>
    `).join('');
  }

  function highlightText(text, query) {
    if (!query || !text) return text;
    const regex = new RegExp(`(${escapeRegExp(query)})`, 'gi');
    return text.replace(regex, '<mark>$1</mark>');
  }

  function escapeRegExp(string) {
    return string.replace(/[.*+?^${}()|[\]\\]/g, '\\$&');
  }

  // Event listeners
  searchInput.addEventListener('input', function() {
    clearTimeout(searchTimeout);
    searchTimeout = setTimeout(performSearch, 300);
  });

  searchButton.addEventListener('click', performSearch);

  [categoryFilter, typeFilter, roleFilter].forEach(filter => {
    filter.addEventListener('change', performSearch);
  });

  clearSearch.addEventListener('click', function() {
    searchInput.value = '';
    categoryFilter.value = '';
    typeFilter.value = '';
    roleFilter.value = '';
    showEmptyState();
  });

  suggestionTags.forEach(tag => {
    tag.addEventListener('click', function() {
      searchInput.value = this.dataset.search;
      performSearch();
    });
  });

  // Handle URL parameters for direct search
  const urlParams = new URLSearchParams(window.location.search);
  const queryParam = urlParams.get('q');
  if (queryParam) {
    searchInput.value = queryParam;
    performSearch();
  }
});
</script>

<style>
.search-container {
  max-width: 800px;
  margin: 0 auto;
  padding: 2rem 1rem;
}

.search-header {
  text-align: center;
  margin-bottom: 2rem;
}

.search-header h2 {
  margin: 0 0 0.5rem 0;
  color: #2c3e50;
}

.search-header p {
  color: #6c757d;
  font-size: 1.1rem;
  margin: 0;
}

.search-form {
  background: white;
  border-radius: 0.5rem;
  padding: 2rem;
  box-shadow: 0 2px 8px rgba(0,0,0,0.1);
  margin-bottom: 2rem;
}

.search-input-container {
  position: relative;
  margin-bottom: 1.5rem;
}

#search-input {
  width: 100%;
  padding: 1rem 4rem 1rem 1.5rem;
  border: 2px solid #e9ecef;
  border-radius: 2rem;
  font-size: 1.1rem;
  transition: border-color 0.2s ease;
}

#search-input:focus {
  outline: none;
  border-color: #3498db;
  box-shadow: 0 0 0 3px rgba(52, 152, 219, 0.1);
}

#search-button {
  position: absolute;
  right: 0.75rem;
  top: 50%;
  transform: translateY(-50%);
  background: #3498db;
  border: none;
  border-radius: 50%;
  width: 2.5rem;
  height: 2.5rem;
  display: flex;
  align-items: center;
  justify-content: center;
  cursor: pointer;
  transition: background-color 0.2s ease;
}

#search-button:hover {
  background-color: #2980b9;
}

#search-button svg {
  fill: white;
}

.search-filters {
  display: flex;
  gap: 1rem;
  margin-bottom: 1.5rem;
  flex-wrap: wrap;
}

.filter-group {
  display: flex;
  align-items: center;
  gap: 0.5rem;
}

.filter-label {
  font-weight: 500;
  color: #2c3e50;
  font-size: 0.9rem;
}

.filter-select {
  padding: 0.5rem;
  border: 1px solid #dee2e6;
  border-radius: 0.25rem;
  background: white;
  font-size: 0.9rem;
  min-width: 150px;
}

.search-suggestions {
  display: flex;
  align-items: center;
  gap: 0.75rem;
  flex-wrap: wrap;
}

.suggestions-label {
  font-size: 0.9rem;
  color: #6c757d;
  font-weight: 500;
}

.suggestion-tag {
  background: #f8f9fa;
  border: 1px solid #dee2e6;
  border-radius: 1rem;
  padding: 0.25rem 0.75rem;
  font-size: 0.85rem;
  cursor: pointer;
  transition: all 0.2s ease;
}

.suggestion-tag:hover {
  background: #e9ecef;
  border-color: #3498db;
  color: #3498db;
}

.search-results {
  background: white;
  border-radius: 0.5rem;
  box-shadow: 0 2px 8px rgba(0,0,0,0.1);
  overflow: hidden;
}

.results-header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 1.5rem 2rem;
  border-bottom: 1px solid #e9ecef;
  background: #f8f9fa;
}

.results-header h3 {
  margin: 0;
  color: #2c3e50;
}

.clear-button {
  background: none;
  border: 1px solid #6c757d;
  border-radius: 0.25rem;
  padding: 0.5rem 1rem;
  color: #6c757d;
  cursor: pointer;
  font-size: 0.9rem;
  transition: all 0.2s ease;
}

.clear-button:hover {
  background: #6c757d;
  color: white;
}

.results-container {
  padding: 1rem 2rem 2rem 2rem;
}

.result-item {
  padding: 1.5rem 0;
  border-bottom: 1px solid #f1f3f4;
}

.result-item:last-child {
  border-bottom: none;
}

.result-title {
  margin: 0 0 0.5rem 0;
}

.result-title a {
  color: #3498db;
  text-decoration: none;
  font-size: 1.1rem;
}

.result-title a:hover {
  text-decoration: underline;
}

.result-description {
  color: #2c3e50;
  margin: 0 0 0.5rem 0;
  font-weight: 500;
}

.result-excerpt {
  color: #6c757d;
  margin: 0 0 0.75rem 0;
  line-height: 1.5;
}

.result-meta {
  display: flex;
  gap: 1rem;
  font-size: 0.85rem;
}

.result-category {
  background: #e3f2fd;
  color: #1976d2;
  padding: 0.2rem 0.5rem;
  border-radius: 0.25rem;
  font-weight: 500;
}

.result-tags {
  color: #6c757d;
}

.search-empty, .search-loading {
  text-align: center;
  padding: 3rem 2rem;
}

.empty-state {
  max-width: 500px;
  margin: 0 auto;
}

.empty-icon {
  fill: #bdc3c7;
  margin-bottom: 1rem;
}

.empty-state h3 {
  color: #2c3e50;
  margin: 0 0 1rem 0;
}

.empty-state p {
  color: #6c757d;
  margin: 0 0 2rem 0;
  line-height: 1.6;
}

.search-tips {
  text-align: left;
  background: #f8f9fa;
  border-radius: 0.5rem;
  padding: 1.5rem;
  border-left: 4px solid #3498db;
}

.search-tips h4 {
  margin: 0 0 1rem 0;
  color: #2c3e50;
}

.search-tips ul {
  margin: 0;
  padding-left: 1.2rem;
}

.search-tips li {
  margin-bottom: 0.5rem;
  color: #6c757d;
  line-height: 1.5;
}

.loading-spinner {
  width: 2rem;
  height: 2rem;
  border: 3px solid #e9ecef;
  border-top-color: #3498db;
  border-radius: 50%;
  animation: spin 1s linear infinite;
  margin: 0 auto 1rem auto;
}

@keyframes spin {
  to { transform: rotate(360deg); }
}

.no-results {
  text-align: center;
  padding: 2rem;
  color: #6c757d;
}

mark {
  background: #fff3cd;
  padding: 0.1rem 0.2rem;
  border-radius: 0.2rem;
}

@media (max-width: 768px) {
  .search-container {
    padding: 1rem;
  }
  
  .search-form {
    padding: 1.5rem;
  }
  
  .search-filters {
    flex-direction: column;
    align-items: stretch;
  }
  
  .filter-group {
    justify-content: space-between;
  }
  
  .filter-select {
    min-width: auto;
    flex: 1;
  }
  
  .results-header {
    flex-direction: column;
    gap: 1rem;
    align-items: flex-start;
  }
  
  .results-container {
    padding: 1rem;
  }
}
</style>