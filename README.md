import { Card, CardContent } from "@/components/ui/card"
import { Input } from "@/components/ui/input"
import { Button } from "@/components/ui/button"
import { Label } from "@/components/ui/label"
import { Calendar } from "@/components/ui/calendar"
import { useState } from "react"
import { format } from "date-fns"

export default function TeachPayBind() {
  const [phone, setPhone] = useState("")
  const [mpin, setMpin] = useState("")
  const [newMpin, setNewMpin] = useState("")
  const [fullName, setFullName] = useState("")
  const [birthday, setBirthday] = useState<Date | undefined>(undefined)
  const [email, setEmail] = useState("")
  const [regDate, setRegDate] = useState<Date | undefined>(undefined)

  const handleSubmit = () => {
    const data = {
      phone,
      mpin,
      newMpin,
      fullName,
      birthday: birthday ? format(birthday, "yyyy-MM-dd") : null,
      email,
      regDate: regDate ? format(regDate, "yyyy-MM-dd") : null,
    }
    console.log("Submitted data:", data)
    // Replace with real Firebase POST logic here
  }

  return (
    <div className="min-h-screen flex items-center justify-center bg-gray-100 p-4">
      <Card className="w-full max-w-xl">
        <CardContent className="space-y-4 p-6">
          <h2 className="text-xl font-semibold text-center">TeachPay 綁卡系統</h2>

          <div>
            <Label>手機號碼</Label>
            <Input value={phone} onChange={(e) => setPhone(e.target.value)} placeholder="09xxxxxxxxx" />
          </div>

          <div>
            <Label>舊 MPIN</Label>
            <Input type="password" value={mpin} onChange={(e) => setMpin(e.target.value)} />
          </div>

          <div>
            <Label>新 MPIN（若不更改可留空）</Label>
            <Input type="password" value={newMpin} onChange={(e) => setNewMpin(e.target.value)} />
          </div>

          <div>
            <Label>GCash 註冊日期</Label>
            <Calendar mode="single" selected={regDate} onSelect={setRegDate} className="rounded-md border" />
          </div>

          <div>
            <Label>持卡人姓名</Label>
            <Input value={fullName} onChange={(e) => setFullName(e.target.value)} />
          </div>

          <div>
            <Label>生日</Label>
            <Calendar mode="single" selected={birthday} onSelect={setBirthday} className="rounded-md border" />
          </div>

          <div>
            <Label>Email</Label>
            <Input value={email} onChange={(e) => setEmail(e.target.value)} />
          </div>

          <Button onClick={handleSubmit} className="w-full">送出資料</Button>
        </CardContent>
      </Card>
    </div>
  )
}
