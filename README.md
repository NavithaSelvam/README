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
# Use an official Python runtime as a parent image
FROM python:3.9-slim

# Set the working directory in the container
WORKDIR /app

# Copy the current directory contents into the container at /app
COPY . /app

# Install any needed packages specified in requirements.txt
RUN pip install flask

# Make port 5000 available to the world outside this container
EXPOSE 5000

# Define environment variable
ENV NAME ToDoApp

# Run app.py when the container launches
CMD ["python", "app.py"]
