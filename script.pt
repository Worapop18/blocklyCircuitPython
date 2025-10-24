// ---------- Workspace Setup ----------
const workspace = Blockly.inject('blocklyDiv', {
  toolbox: document.getElementById('toolbox'),
  trashcan: true,
  zoom: { controls: true, wheel: true },
});

// ---------- Define Custom Blocks ----------
Blockly.defineBlocksWithJsonArray([
  { "type": "start_code", "message0": "เริ่มโปรแกรม", "nextStatement": null, "colour": 120, "tooltip": "เริ่มต้นโปรแกรม CircuitPython" },
  { "type": "led_on", "message0": "เปิดไฟ LED", "previousStatement": null, "nextStatement": null, "colour": 290 },
  { "type": "led_off", "message0": "ปิดไฟ LED", "previousStatement": null, "nextStatement": null, "colour": 290 },
  { "type": "sleep_block", "message0": "หน่วงเวลา %1 วินาที", "args0":[{"type":"field_number","name":"SECONDS","value":1,"min":0}], "previousStatement": null, "nextStatement": null, "colour": 30 },
  { "type": "button_read", "message0": "อ่านค่าปุ่มกด (GP14)", "output": "Boolean", "colour": 230 }
]);

// ---------- Auto Update Code (Block as Text) ----------
const codeOutput = document.getElementById("code-output");

function updateCodeDisplay() {
  const allBlocks = workspace.getAllBlocks();
  if(allBlocks.length === 0) {
    codeOutput.textContent = '# ลากบล็อกมาเพื่อสร้างโปรแกรม';
    return;
  }

  // สร้างข้อความแทนแต่ละบล็อก
  let codeLines = allBlocks.map(block => {
    let extra = '';
    // ถ้ามี field เช่น SECONDS ให้เอามาแสดง
    if(block.getFieldValue('SECONDS') !== null) {
      extra = ` (${block.getFieldValue('SECONDS')} วินาที)`;
    }
    return `# [${block.type}]${extra}`;
  });

  codeOutput.textContent = codeLines.join('\n');
}

workspace.addChangeListener(updateCodeDisplay);
updateCodeDisplay();

// ---------- Buttons ----------
document.getElementById("clearBtn").onclick = () => { workspace.clear(); updateCodeDisplay(); };
document.getElementById("exportBtn").onclick = () => { navigator.clipboard.writeText(codeOutput.textContent); alert("คัดลอกโค้ดไป clipboard แล้ว!"); };
document.getElementById("runBtn").onclick = () => {
  const result = document.getElementById("runResult");
  const code = codeOutput.textContent;
  result.textContent = code.trim() === '' || code.startsWith('#') ? '⚠️ ไม่มีโค้ดให้รัน' : '🚀 (โค้ดจำลอง)\n\n' + code;
};
