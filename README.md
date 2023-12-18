### Flexmoney

## Frontend(React):-
# Create React App:
npx create-react-app yoga-admission-form
cd yoga-admission-form
# Install Axios (for API calls):
Install Axios (for API calls):
npm install axios
# Modify src/App.js:
import React, { useState } from 'react';
import axios from 'axios';

const App = () => {
  const [formData, setFormData] = useState({
    name: '',
    age: '',
    selectedBatch: '',
  });

  const handleInputChange = (e) => {
    setFormData({ ...formData, [e.target.name]: e.target.value });
  };

  const handleSubmit = async (e) => {
    e.preventDefault();
    try {
      const response = await axios.post('http://localhost:5000/enroll', formData);
      console.log(response.data);
    } catch (error) {
      console.error('Error:', error.message);
    }
  };

  return (
    <div>
      <h1>Yoga Admission Form</h1>
      <form onSubmit={handleSubmit}>
        <label>Name:</label>
        <input type="text" name="name" onChange={handleInputChange} required />
        <br />
        <label>Age:</label>
        <input type="number" name="age" onChange={handleInputChange} required />
        <br />
        <label>Select Batch:</label>
        <select name="selectedBatch" onChange={handleInputChange} required>
          <option value="">Select Batch</option>
          <option value="6-7AM">6-7AM</option>
          <option value="7-8AM">7-8AM</option>
          <option value="8-9AM">8-9AM</option>
          <option value="5-6PM">5-6PM</option>
        </select>
        <br />
        <button type="submit">Enroll</button>
      </form>
    </div>
  );
};

export default App;



## Backend (Node.js with Express)
# Create package.json for the backend:
npm init -y
npm install express body-parser
# Create server.js:
const express = require('express');
const bodyParser = require('body-parser');

const app = express();
const PORT = process.env.PORT || 5000;

app.use(bodyParser.json());

const enrolledUsers = [];

app.post('/enroll', (req, res) => {
  const { name, age, selectedBatch } = req.body;

  // Basic validations
  if (!name || !age || !selectedBatch) {
    return res.status(400).json({ message: 'Name, age, and batch are required fields.' });
  }

  const user = { name, age, selectedBatch };
  enrolledUsers.push(user);

  // Assuming a function to complete the payment
  // const paymentResponse = CompletePayment(user, paymentDetails);

  return res.status(200).json({ message: 'Enrollment successful!' });
});

app.listen(PORT, () => {
  console.log(`Server is running on port ${PORT}`);
});

# ER Diagram
Creating a complete ER (Entity-Relationship) diagram for the given scenario would involve defining entities, their attributes, and relationships between them. In this case, we can identify at least two entities: "Participant" and "Batch."

Here is a simplified ER diagram:

 
+------------------+      +------------------+
|   Participant   |      |      Batch       |
+------------------+      +------------------+
| participant_id  |      | batch_id         |
| name            |      | start_time       |
| age             |      | end_time         |
| selected_batch  |      +------------------+
| payment_status  |
+------------------+
# Explanation:

Participant Entity:

participant_id: Unique identifier for each participant (primary key).
name: Name of the participant.
age: Age of the participant.
selected_batch: The batch chosen by the participant.
payment_status: Status of the payment for the participant.

Batch Entity:

batch_id: Unique identifier for each batch (primary key).
start_time: Start time of the batch.
end_time: End time of the batch.
Relationships:

There is a relationship between the "Participant" and "Batch" entities based on the "selected_batch" attribute. This relationship indicates which batch a participant has selected.



