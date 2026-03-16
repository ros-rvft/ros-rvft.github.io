---
title: "Tool Directory"
permalink: /tools
layout: single
sidebar:
  nav: "guidelines"
---

A comprehensive directory of tools mentioned across the ROS-RVFT guidelines. Each tool is linked to the guideline(s) where it is discussed. Use the filters below to narrow by category or ROS version.

<div style="margin: 16px 0; display: flex; gap: 12px; flex-wrap: wrap; align-items: center;">
  <input type="text" id="tool-search" placeholder="Search tools…" style="padding: 6px 12px; border: 1px solid #ccc; border-radius: 4px; font-size: 14px; flex: 1; min-width: 180px;">
  <select id="category-filter" style="padding: 6px 12px; border: 1px solid #ccc; border-radius: 4px; font-size: 14px;">
    <option value="">All categories</option>
  </select>
  <select id="ros-filter" style="padding: 6px 12px; border: 1px solid #ccc; border-radius: 4px; font-size: 14px;">
    <option value="">All ROS versions</option>
    <option value="ROS 1">ROS 1</option>
    <option value="ROS 2">ROS 2</option>
  </select>
</div>

<table id="tool-table" style="width: 100%; border-collapse: collapse; font-size: 14px;">
  <thead>
    <tr style="border-bottom: 2px solid #ddd; text-align: left;">
      <th style="padding: 8px;">Tool</th>
      <th style="padding: 8px;">Category</th>
      <th style="padding: 8px;">Guideline(s)</th>
      <th style="padding: 8px;">ROS</th>
    </tr>
  </thead>
  <tbody>
    {% for tool in site.data.tools %}
    <tr class="tool-row" data-category="{{ tool.category }}" data-ros="{{ tool.ros_versions | join: ',' }}" data-name="{{ tool.name | downcase }}">
      <td style="padding: 8px;">{% if tool.url != "" %}<a href="{{ tool.url }}">{{ tool.name }}</a>{% else %}{{ tool.name }}{% endif %}<br><small style="color: #666;">{{ tool.description }}</small></td>
      <td style="padding: 8px;">{{ tool.category }}</td>
      <td style="padding: 8px;">{% for g in tool.guidelines %}<a href="{{ g.url }}">{{ g.id }}</a>{% unless forloop.last %}, {% endunless %}{% endfor %}</td>
      <td style="padding: 8px;">{{ tool.ros_versions | join: ", " }}</td>
    </tr>
    {% endfor %}
  </tbody>
</table>

<p id="no-results" style="display: none; color: #666; font-style: italic;">No tools match the current filters.</p>

<script>
document.addEventListener('DOMContentLoaded', function() {
  var rows = document.querySelectorAll('.tool-row');
  var searchInput = document.getElementById('tool-search');
  var categoryFilter = document.getElementById('category-filter');
  var rosFilter = document.getElementById('ros-filter');
  var noResults = document.getElementById('no-results');

  // Populate category dropdown
  var categories = {};
  rows.forEach(function(row) {
    var cat = row.getAttribute('data-category');
    if (cat) categories[cat] = true;
  });
  Object.keys(categories).sort().forEach(function(cat) {
    var opt = document.createElement('option');
    opt.value = cat;
    opt.textContent = cat;
    categoryFilter.appendChild(opt);
  });

  function filterRows() {
    var search = searchInput.value.toLowerCase();
    var cat = categoryFilter.value;
    var ros = rosFilter.value;
    var visible = 0;

    rows.forEach(function(row) {
      var name = row.getAttribute('data-name');
      var rowCat = row.getAttribute('data-category');
      var rowRos = row.getAttribute('data-ros');
      var show = true;

      if (search && name.indexOf(search) === -1 && row.textContent.toLowerCase().indexOf(search) === -1) show = false;
      if (cat && rowCat !== cat) show = false;
      if (ros && rowRos.indexOf(ros) === -1) show = false;

      row.style.display = show ? '' : 'none';
      if (show) visible++;
    });

    noResults.style.display = visible === 0 ? '' : 'none';
  }

  searchInput.addEventListener('input', filterRows);
  categoryFilter.addEventListener('change', filterRows);
  rosFilter.addEventListener('change', filterRows);
});
</script>
