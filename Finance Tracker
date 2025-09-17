<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Personal Finance Tracker</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;500;600;700&display=swap" rel="stylesheet">
    <style>
        body {
            font-family: 'Inter', sans-serif;
        }
        .modal-backdrop {
            display: none;
            position: fixed;
            top: 0;
            left: 0;
            right: 0;
            bottom: 0;
            background-color: rgba(0, 0, 0, 0.5);
            justify-content: center;
            align-items: center;
            z-index: 50;
        }
        .modal-backdrop.flex {
            display: flex;
        }
    </style>
</head>
<body class="bg-slate-100 text-slate-800">

    <div class="container mx-auto p-4 md:p-8 max-w-4xl">
        <header class="text-center mb-10">
            <h1 class="text-4xl md:text-5xl font-bold text-slate-900">Finance Tracker</h1>
            <p class="text-slate-500 mt-3">Your personal dashboard for income and expenses.</p>
        </header>

        <main>
            <!-- Summary Cards -->
            <section class="grid grid-cols-1 md:grid-cols-3 gap-6 mb-10">
                <div class="bg-teal-50 p-6 rounded-xl shadow-sm border-l-4 border-teal-500">
                    <h2 class="text-lg font-semibold text-slate-600">Total Income</h2>
                    <p id="total-income" class="text-3xl font-bold text-teal-600 mt-2">₹0.00</p>
                </div>
                <div class="bg-orange-50 p-6 rounded-xl shadow-sm border-l-4 border-orange-500">
                    <h2 class="text-lg font-semibold text-slate-600">Total Expenses</h2>
                    <p id="total-expenses" class="text-3xl font-bold text-orange-600 mt-2">₹0.00</p>
                </div>
                <div class="bg-white p-6 rounded-xl shadow-sm border border-l-4 border-indigo-500">
                    <h2 class="text-lg font-semibold text-slate-600">Net Balance</h2>
                    <p id="net-balance" class="text-3xl font-bold text-indigo-600 mt-2">₹0.00</p>
                </div>
            </section>

            <!-- Add Transaction Form -->
            <section class="bg-white p-6 rounded-xl shadow-sm mb-10">
                <h2 class="text-2xl font-bold mb-4 text-slate-800">Add New Transaction</h2>
                <form id="transaction-form" class="grid grid-cols-1 md:grid-cols-4 gap-4 items-end">
                    <div class="md:col-span-2">
                        <label for="description" class="block text-sm font-medium text-slate-700">Description</label>
                        <input type="text" id="description" placeholder="e.g., Salary, Groceries" class="mt-1 block w-full px-4 py-2 bg-slate-50 border border-slate-300 rounded-lg shadow-sm focus:outline-none focus:ring-2 focus:ring-teal-500 focus:border-teal-500" required>
                    </div>
                    <div>
                        <label for="amount" class="block text-sm font-medium text-slate-700">Amount</label>
                        <input type="number" id="amount" placeholder="250.00" min="0.01" step="0.01" class="mt-1 block w-full px-4 py-2 bg-slate-50 border border-slate-300 rounded-lg shadow-sm focus:outline-none focus:ring-2 focus:ring-teal-500 focus:border-teal-500" required>
                    </div>
                    <div>
                        <label for="type" class="block text-sm font-medium text-slate-700">Type</label>
                        <select id="type" class="mt-1 block w-full px-4 py-2 bg-slate-50 border border-slate-300 rounded-lg shadow-sm focus:outline-none focus:ring-2 focus:ring-teal-500 focus:border-teal-500">
                            <option value="income">Income</option>
                            <option value="expense">Expense</option>
                        </select>
                    </div>
                    <div class="md:col-span-4 flex justify-end">
                         <button type="submit" class="w-full md:w-auto inline-flex justify-center py-2 px-6 border border-transparent shadow-sm text-sm font-medium rounded-lg text-white bg-teal-600 hover:bg-teal-700 focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-teal-500">
                            Add Transaction
                        </button>
                    </div>
                </form>
            </section>

            <!-- Transactions List -->
            <section class="bg-white p-6 rounded-xl shadow-sm">
                <h2 class="text-2xl font-bold mb-4 text-slate-800">Transaction History</h2>
                <div class="overflow-x-auto">
                    <table class="min-w-full">
                        <thead class="border-b-2 border-slate-200">
                            <tr>
                                <th scope="col" class="px-6 py-3 text-left text-xs font-medium text-slate-500 uppercase tracking-wider">Description</th>
                                <th scope="col" class="px-6 py-3 text-left text-xs font-medium text-slate-500 uppercase tracking-wider">Amount</th>
                                <th scope="col" class="px-6 py-3 text-left text-xs font-medium text-slate-500 uppercase tracking-wider">Type</th>
                                <th scope="col" class="px-6 py-3 text-right text-xs font-medium text-slate-500 uppercase tracking-wider">Actions</th>
                            </tr>
                        </thead>
                        <tbody id="transaction-list" class="bg-white">
                            <!-- JS will populate this -->
                        </tbody>
                    </table>
                </div>
            </section>
        </main>
    </div>

    <!-- Edit Modal -->
    <div id="edit-modal" class="modal-backdrop">
        <div class="bg-white rounded-xl shadow-xl w-full max-w-md m-4">
            <div class="p-8">
                <h3 class="text-2xl font-bold mb-6 text-slate-800">Edit Transaction</h3>
                <form id="edit-form">
                    <input type="hidden" id="edit-id">
                    <div class="mb-4">
                        <label for="edit-description" class="block text-sm font-medium text-slate-700">Description</label>
                        <input type="text" id="edit-description" class="mt-1 block w-full px-4 py-2 bg-slate-50 border border-slate-300 rounded-lg shadow-sm focus:outline-none focus:ring-2 focus:ring-teal-500 focus:border-teal-500" required>
                    </div>
                    <div class="mb-4">
                        <label for="edit-amount" class="block text-sm font-medium text-slate-700">Amount</label>
                        <input type="number" id="edit-amount" min="0.01" step="0.01" class="mt-1 block w-full px-4 py-2 bg-slate-50 border border-slate-300 rounded-lg shadow-sm focus:outline-none focus:ring-2 focus:ring-teal-500 focus:border-teal-500" required>
                    </div>
                    <div class="mb-6">
                        <label for="edit-type" class="block text-sm font-medium text-slate-700">Type</label>
                        <select id="edit-type" class="mt-1 block w-full px-4 py-2 bg-slate-50 border border-slate-300 rounded-lg shadow-sm focus:outline-none focus:ring-2 focus:ring-teal-500 focus:border-teal-500">
                            <option value="income">Income</option>
                            <option value="expense">Expense</option>
                        </select>
                    </div>
                    <div class="flex justify-end space-x-4">
                        <button type="button" id="cancel-edit" class="py-2 px-4 border border-slate-300 rounded-lg shadow-sm text-sm font-medium text-slate-700 bg-white hover:bg-slate-50">Cancel</button>
                        <button type="submit" class="py-2 px-4 border border-transparent rounded-lg shadow-sm text-sm font-medium text-white bg-teal-600 hover:bg-teal-700">Save Changes</button>
                    </div>
                </form>
            </div>
        </div>
    </div>


    <script>
        document.addEventListener('DOMContentLoaded', function() {
            var transactionForm = document.getElementById('transaction-form');
            var transactionList = document.getElementById('transaction-list');
            var totalIncomeEl = document.getElementById('total-income');
            var totalExpensesEl = document.getElementById('total-expenses');
            var netBalanceEl = document.getElementById('net-balance');

            var editModal = document.getElementById('edit-modal');
            var editForm = document.getElementById('edit-form');
            var cancelEditBtn = document.getElementById('cancel-edit');
            var editIdInput = document.getElementById('edit-id');
            var editDescriptionInput = document.getElementById('edit-description');
            var editAmountInput = document.getElementById('edit-amount');
            var editTypeInput = document.getElementById('edit-type');
            
            var transactions = [];

            function renderTransactions() {
                transactionList.innerHTML = '';
                
                if (transactions.length === 0) {
                    transactionList.innerHTML = '<tr><td colspan="4" class="text-center text-slate-500 py-6">No transactions yet. Add one to get started!</td></tr>';
                } else {
                    for (var i = 0; i < transactions.length; i++) {
                        var transaction = transactions[i];
                        var isIncome = transaction.type === 'income';
                        var amountColor = isIncome ? 'text-teal-600' : 'text-orange-600';
                        var sign = isIncome ? '+' : '-';

                        var row = document.createElement('tr');
                        row.className = 'border-b border-slate-200 hover:bg-slate-50';

                        var rowHTML = 
                            '<td class="px-6 py-4 whitespace-nowrap">' +
                                '<div class="text-sm font-medium text-slate-900">' + transaction.description + '</div>' +
                            '</td>' +
                            '<td class="px-6 py-4 whitespace-nowrap">' +
                                '<div class="text-sm font-semibold ' + amountColor + '">' + sign + ' ₹' + Math.abs(transaction.amount).toFixed(2) + '</div>' +
                            '</td>' +
                            '<td class="px-6 py-4 whitespace-nowrap">' +
                                '<span class="px-2.5 py-0.5 inline-flex text-xs leading-5 font-semibold rounded-full ' + (isIncome ? 'bg-teal-100 text-teal-800' : 'bg-orange-100 text-orange-800') + '">' +
                                    transaction.type +
                                '</span>' +
                            '</td>' +
                            '<td class="px-6 py-4 whitespace-nowrap text-right text-sm font-medium">' +
                                '<button onclick="showEditModal(' + transaction.id + ')" class="text-indigo-600 hover:text-indigo-800 mr-4 transition-colors duration-200">' +
                                    '<svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5" viewBox="0 0 20 20" fill="currentColor"><path d="M17.414 2.586a2 2 0 00-2.828 0L7 10.172V13h2.828l7.586-7.586a2 2 0 000-2.828z" /><path fill-rule="evenodd" d="M2 6a2 2 0 012-2h4a1 1 0 010 2H4v10h10v-4a1 1 0 112 0v4a2 2 0 01-2 2H4a2 2 0 01-2-2V6z" clip-rule="evenodd" /></svg>' +
                                '</button>' +
                                '<button onclick="deleteTransaction(' + transaction.id + ')" class="text-red-600 hover:text-red-800 transition-colors duration-200">' +
                                    '<svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5" viewBox="0 0 20 20" fill="currentColor"><path fill-rule="evenodd" d="M9 2a1 1 0 00-.894.553L7.382 4H4a1 1 0 000 2v10a2 2 0 002 2h8a2 2 0 002-2V6a1 1 0 100-2h-3.382l-.724-1.447A1 1 0 0011 2H9zM7 8a1 1 0 012 0v6a1 1 0 11-2 0V8zm4 0a1 1 0 012 0v6a1 1 0 11-2 0V8z" clip-rule="evenodd" /></svg>' +
                                '</button>' +
                            '</td>';
                        
                        row.innerHTML = rowHTML;
                        transactionList.appendChild(row);
                    }
                }
                updateSummary();
            }

            function updateSummary() {
                var totalIncome = 0;
                var totalExpenses = 0;
                for (var i = 0; i < transactions.length; i++) {
                    var transaction = transactions[i];
                    if (transaction.type === 'income') {
                        totalIncome = totalIncome + transaction.amount;
                    } else if (transaction.type === 'expense') {
                        totalExpenses = totalExpenses + transaction.amount;
                    }
                }
                var balance = totalIncome - totalExpenses;

                totalIncomeEl.textContent = '₹' + totalIncome.toFixed(2);
                totalExpensesEl.textContent = '₹' + totalExpenses.toFixed(2);
                netBalanceEl.textContent = '₹' + balance.toFixed(2);
                
                if (balance < 0) {
                    netBalanceEl.classList.add('text-orange-600');
                    netBalanceEl.classList.remove('text-indigo-600');
                } else {
                    netBalanceEl.classList.add('text-indigo-600');
                    netBalanceEl.classList.remove('text-orange-600');
                }
            }

            function addTransaction(event) {
                event.preventDefault();
                var description = document.getElementById('description').value;
                var amount = parseFloat(document.getElementById('amount').value);
                var type = document.getElementById('type').value;

                if (description.trim() === '' || isNaN(amount) || amount <= 0) {
                    console.error('Invalid input');
                    return;
                }
                var newTransaction = {
                    id: Date.now(),
                    description: description,
                    amount: amount,
                    type: type,
                };
                transactions.push(newTransaction);
                renderTransactions();
                transactionForm.reset();
            }

            window.deleteTransaction = function(transactionIdToDelete) {
                var updatedTransactions = [];
                for (var i = 0; i < transactions.length; i++) {
                    var currentTransaction = transactions[i];
                    if (currentTransaction.id !== transactionIdToDelete) {
                        updatedTransactions.push(currentTransaction);
                    }
                }
                transactions = updatedTransactions;
                renderTransactions();
            }

            window.showEditModal = function(id) {
                var transactionToEdit;
                for (var i = 0; i < transactions.length; i++) {
                    if (transactions[i].id === id) {
                        transactionToEdit = transactions[i];
                        break;
                    }
                }
                
                if (transactionToEdit) {
                    editIdInput.value = transactionToEdit.id;
                    editDescriptionInput.value = transactionToEdit.description;
                    editAmountInput.value = transactionToEdit.amount;
                    editTypeInput.value = transactionToEdit.type;
                    editModal.classList.add('flex');
                }
            }

            function hideEditModal() {
                 editModal.classList.remove('flex');
            }

            function handleEditSubmit(event) {
                event.preventDefault();
                var id = parseInt(editIdInput.value);
                var updatedDescription = editDescriptionInput.value;
                var updatedAmount = parseFloat(editAmountInput.value);
                var updatedType = editTypeInput.value;
                for (var i = 0; i < transactions.length; i++) {
                    if (transactions[i].id === id) {
                        transactions[i].description = updatedDescription;
                        transactions[i].amount = updatedAmount;
                        transactions[i].type = updatedType;
                        break;
                    }
                }
                renderTransactions();
                hideEditModal();
            }
            
            transactionForm.addEventListener('submit', addTransaction);
            editForm.addEventListener('submit', handleEditSubmit);
            cancelEditBtn.addEventListener('click', hideEditModal);

            renderTransactions();
        });
    </script>

</body>
</html>

