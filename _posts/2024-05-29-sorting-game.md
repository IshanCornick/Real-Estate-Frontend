
<html>
<head>
    <title>Custom Sorting Game</title>
</head>
<body>
    <h2>Custom Sorting Game</h2>
    <p>Enter your list of words separated by commas:</p>
    <input type="text" id="inputList" placeholder="Enter words here">
    <button onclick="sortList()">Sort List</button>

    <ul id="sortable-list">
    </ul>
    <button onclick="checkOrder()">Check Order</button>
    <p id="result"></p>

    <script>
        function sortList() {
            const input = document.getElementById('inputList').value;
            const words = input.split(',').map(word => word.trim());
            const sortedWords = words.sort((a, b) => a.localeCompare(b));
            const sortableList = document.getElementById('sortable-list');
            sortableList.innerHTML = '';
            sortedWords.forEach(word => {
                const li = document.createElement('li');
                li.textContent = word;
                li.draggable = true;
                li.addEventListener('dragstart', handleDragStart);
                sortableList.appendChild(li);
            });
        }

        function handleDragStart(e) {
            e.dataTransfer.effectAllowed = 'move';
            e.dataTransfer.setData('text/html', null);
            e.target.classList.add('dragging');
        }

        // Make the list sortable
        const sortableList = document.getElementById('sortable-list');
        sortableList.addEventListener('dragover', handleDragOver);
        sortableList.addEventListener('drop', handleDrop);

        function handleDragOver(e) {
            e.preventDefault();
            const draggingElement = document.querySelector('.dragging');
            const closestElement = getClosestElement(e.clientY);
            if (closestElement === draggingElement || closestElement.nextSibling === draggingElement) return;
            sortableList.insertBefore(draggingElement, closestElement.nextSibling);
        }

        function handleDrop(e) {
            e.preventDefault();
            const draggingElement = document.querySelector('.dragging');
            const closestElement = getClosestElement(e.clientY);
            sortableList.insertBefore(draggingElement, closestElement.nextSibling);
            draggingElement.classList.remove('dragging');
        }

        function getClosestElement(y) {
            const draggableElements = Array.from(document.querySelectorAll('#sortable-list li:not(.dragging)'));
            return draggableElements.reduce((closest, child) => {
                const box = child.getBoundingClientRect();
                const offset = y - box.top - box.height / 2;
                if (offset < 0 && offset > closest.offset) {
                    return { offset: offset, element: child };
                } else {
                    return closest;
                }
            }, { offset: Number.NEGATIVE_INFINITY }).element;
        }

        function checkOrder() {
            const sortedList = Array.from(document.querySelectorAll('#sortable-list li'))
                .map(item => item.textContent)
                .join('|');
            const expectedOrder = sortedList.split('|').sort().join('|');

            if (sortedList === expectedOrder) {
                document.getElementById('result').innerText = "Congratulations! You sorted the list correctly!";
            } else {
                document.getElementById('result').innerText = "Sorry, the order is incorrect. Try again!";
            }
        }
    </script>
</body>
</html>
