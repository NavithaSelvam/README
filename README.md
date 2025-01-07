from flask import Flask, request, jsonify

app = Flask(__name__)

todos = []

@app.route('/todos', methods=['GET'])
def get_todos():
    return jsonify(todos)

@app.route('/todos', methods=['POST'])
def add_todo():
    new_todo = request.json.get('task')
    todos.append({'task': new_todo})
    return jsonify({'message': 'Todo added!'}), 201

@app.route('/todos/<int:index>', methods=['DELETE'])
def delete_todo(index):
    try:
        todos.pop(index)
        return jsonify({'message': 'Todo deleted!'})
    except IndexError:
        return jsonify({'error': 'Todo not found!'}), 404

if __name__ == '__main__':
    app.run(host='0.0.0.0', port=5000)

FROM python:3.9-slim


WORKDIR /app


COPY . /app


RUN pip install flask

EXPOSE 5000

# Clone the repository
git clone https://github.com/your-username/your-repository-name.git

# Navigate to the repository folder
cd your-repository-name

# Modify the README.md file (or any file)
# Open it in a text editor and make your changes

# Stage the modified file
git add README.md

# Commit the changes
git commit -m "Updated README"

# Push the changes to GitHub
git push origin main

ENV NAME ToDoApp
CMD ["python", "app.py"]
