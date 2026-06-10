const express = require("express");
const User = require("../models/User");
const authenticate = require("../middleware/authMiddleware");
const authorize = require("../middleware/roleMiddleware");

const router = express.Router();

// Get all users (Admin only)
router.get("/", authenticate, authorize(["Admin"]), async (req, res) => {
  const users = await User.findAll();
  res.json(users);
});

// Get user by ID
router.get("/:id", authenticate, async (req, res) => {
  const user = await User.findByPk(req.params.id);
  if (!user) return res.status(404).json({ error: "User not found" });
  res.json(user);
});

// Update user
router.put("/:id", authenticate, async (req, res) => {
  const user = await User.findByPk(req.params.id);
  if (!user) return res.status(404).json({ error: "User not found" });
  await user.update(req.body);
  res.json(user);
});

// Delete user (Admin only)
router.delete("/:id", authenticate, authorize(["Admin"]), async (req, res) => {
  const user = await User.findByPk(req.params.id);
  if (!user) return res.status(404).json({ error: "User not found" });
  await user.destroy();
  res.json({ message: "User deleted successfully" });
});

module.exports = router;
